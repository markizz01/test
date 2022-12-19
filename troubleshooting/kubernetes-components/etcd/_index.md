Этот раздел содержит команды и советы по устранению неполадок нод с ролью etcd.

# 1.Проверяем, запущен ли контейнер etcd

Контейнер для etcd должен иметь статус **Up** . Продолжительность, указанная после **Up** , — это время работы контейнера.
```
docker ps -a -f=name=etcd$
```

Пример вывода:
```
CONTAINER ID        IMAGE                         COMMAND                  CREATED             STATUS              PORTS   NAMES
           
605a124503b9        rancher/coreos-etcd:v3.2.18   "/usr/local/bin/et..."   2 hours ago         Up 2 hours                   etcd      
```

## ETCD регистрация контейнера (Container Logging)

Журнал контейнера может содержать информацию о том, в чем может быть проблема.
```
docker logs etcd
```

|Журнал	|Объяснение|
|-|-|
|health check for peer xxx could not connect: dial tcp IP:2380: getsockopt: connection refused|	Соединение с адресом, указанным в порте 2380, не может быть установлено. Проверьте, запущен ли контейнер etcd на хосте с указанным адресом.|
|xxx is starting a new election at term x|	Кластер etcd потерял кворум и пытается установить нового лидера. Это может произойти, когда большинство нод, на которых запущен etcd, выходят из строя или становятся недоступными.|
|connection error: desc = "transport: Error while dialing dial tcp 0.0.0.0:2379: i/o timeout"; Reconnecting to {0.0.0.0:2379 0 <nil>}	|Брандмауэр хоста препятствует сетевому обмену данными.|
|rafthttp: request cluster ID mismatch|	Узел с логированием etcd rafthttp: request cluster ID mismatch пытается присоединиться к кластеру, который уже был сформирован с другой нодой. Узел должен быть удален из кластера и повторно добавлен.|
|rafthttp: failed to find member	|Состояние кластера ( /var/lib/etcd) содержит неверную информацию для присоединения к кластеру. нода должна быть удалена из кластера, каталог состояния должен быть очищен, а нода должна быть повторно добавлена.|

## etcd Проверка кластера и подключения
 
Адрес, по которому прослушивается etcd, зависит от конфигурации адреса хоста, на котором работает etcd. Если для хоста, на котором запущен etcd, настроен внутренний адрес, конечная точка etcdctl должна быть указана явно. Если какая-либо из команд отвечает Error: context deadline exceeded, экземпляр etcd неисправен (либо кворум потерян, либо экземпляр неправильно присоединен к кластеру).

## Проверить участников etcd на всех нодах
  
Выход должен содержать все узлы с ролью etcd, и выход должен быть идентичен для всех узлов.
  
Команда:
```  
docker exec etcd etcdctl member list
```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```  
docker exec etcd sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT member list"
```
  
Пример вывода:
```  
xxx, started, etcd-xxx, https://IP:2380, https://IP:2379,https://IP:4001
xxx, started, etcd-xxx, https://IP:2380, https://IP:2379,https://IP:4001
xxx, started, etcd-xxx, https://IP:2380, https://IP:2379,https://IP:4001
  ```
  
## Проверить статус конечной точки(Endpoint)
Значения для RAFT TERM должны быть равны и RAFT INDEX не должны быть слишком далеко друг от друга.
  
Команда:
  ```
docker exec -e ETCDCTL_ENDPOINTS=$(docker exec etcd /bin/sh -c "etcdctl member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','") etcd etcdctl endpoint status --write-out table
```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```
  docker exec etcd etcdctl endpoint status --endpoints=$(docker exec etcd /bin/sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','") --write-out table
```
  
  Пример вывода:
```
+-----------------+------------------+---------+---------+-----------+-----------+------------+
| ENDPOINT        |        ID        | VERSION | DB SIZE | IS LEADER | RAFT TERM | RAFT INDEX |
+-----------------+------------------+---------+---------+-----------+-----------+------------+
| https://IP:2379 | 333ef673fc4add56 |  3.2.18 |   24 MB |     false |        72 |      66887 |
| https://IP:2379 | 5feed52d940ce4cf |  3.2.18 |   24 MB |      true |        72 |      66887 |
| https://IP:2379 | db6b3bdb559a848d |  3.2.18 |   25 MB |     false |        72 |      66887 |
+-----------------+------------------+---------+---------+-----------+-----------+------------+
```
           
# Проверить работоспособность конечной точки
  
Команда:
```  
docker exec -e ETCDCTL_ENDPOINTS=$(docker exec etcd /bin/sh -c "etcdctl member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','") etcd etcdctl endpoint health
```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```
  docker exec etcd etcdctl endpoint health --endpoints=$(docker exec etcd /bin/sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','")
```
  Пример вывода:
```  
https://IP:2379 is healthy: successfully committed proposal: took = 2.113189ms
https://IP:2379 is healthy: successfully committed proposal: took = 2.649963ms
https://IP:2379 is healthy: successfully committed proposal: took = 2.451201ms
```
  
## Проверьте подключение к порту TCP/2379.
  
Команда:
```  
for endpoint in $(docker exec etcd /bin/sh -c "etcdctl member list | cut -d, -f5"); do
   echo "Validating connection to ${endpoint}/health"
   docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl -s -w "\n" --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) "${endpoint}/health"
done
```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```
  for endpoint in $(docker exec etcd /bin/sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT member list | cut -d, -f5"); do
  echo "Validating connection to ${endpoint}/health";
  docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl -s -w "\n" --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) "${endpoint}/health"
done
```
  
Пример вывода:
```  
Validating connection to https://IP:2379/health
{"health": "true"}
Validating connection to https://IP:2379/health
{"health": "true"}
Validating connection to https://IP:2379/health
{"health": "true"}
```
  
## Проверьте подключение к порту TCP/2380.
  
Команда:
```  
for endpoint in $(docker exec etcd /bin/sh -c "etcdctl member list | cut -d, -f4"); do
  echo "Validating connection to ${endpoint}/version";
  docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl --http1.1 -s -w "\n" --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) "${endpoint}/version"
done
```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```  
for endpoint in $(docker exec etcd /bin/sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT member list | cut -d, -f4"); do
  echo "Validating connection to ${endpoint}/version";
  docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl --http1.1 -s -w "\n" --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) "${endpoint}/version"
done
```  
Пример вывода:
```  
Validating connection to https://IP:2380/version
{"etcdserver":"3.2.18","etcdcluster":"3.2.0"}
Validating connection to https://IP:2380/version
{"etcdserver":"3.2.18","etcdcluster":"3.2.0"}
Validating connection to https://IP:2380/version
{"etcdserver":"3.2.18","etcdcluster":"3.2.0"}
```
  
## Etcd Alarms (Сигналы тревоги)
etcd запустит сигнал тревоги, например, когда закончится место.
  
Команда:
```  
docker exec etcd etcdctl alarm list
```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```  
docker exec etcd sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT alarm list"
```
  
Пример вывода при срабатывании тревоги NOSPACE:
```  
memberID:x alarm:NOSPACE
memberID:x alarm:NOSPACE
memberID:x alarm:NOSPACE
```
  
## etcd Space Errors (ошибки в пространстве)
  
Связанные сообщения об ошибках etcdserver: mvcc: database space exceededили applying raft message exceeded backend quota. Тревога(Alarm) NOSPACE сработает.

Резолюции:
-	Сжать Keyspace (ключевое пространство)
-	Дефрагментировать всех участников etcd
-	Проверить Endpoint Status (статус конечной точки)
-	Снять Alarm (тревогу)
  
## Сжать Keyspace (ключевое пространство)
Команда:
  ```
rev=$(docker exec etcd etcdctl endpoint status --write-out json | egrep -o '"revision":[0-9]*' | egrep -o '[0-9]*')
docker exec etcd etcdctl compact "$rev"
  ```
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
  ```
rev=$(docker exec etcd sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT endpoint status --write-out json | egrep -o '\"revision\":[0-9]*' | egrep -o '[0-9]*'")
docker exec etcd sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT compact \"$rev\""
  ```
Пример вывода:
  ```
compacted revision xxx
  ```
## Дефрагментировать всех участников etcd
Команда:
  ```
docker exec -e ETCDCTL_ENDPOINTS=$(docker exec etcd /bin/sh -c "etcdctl member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','") etcd etcdctl defrag
  ```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
  ```
docker exec etcd sh -c "etcdctl defrag --endpoints=$(docker exec etcd /bin/sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','")"
```
  Пример вывода:
  ```
Finished defragmenting etcd member[https://IP:2379]
Finished defragmenting etcd member[https://IP:2379]
Finished defragmenting etcd member[https://IP:2379]
  ```
## Проверить статус конечной точки
  
Команда:
  ```
docker exec -e ETCDCTL_ENDPOINTS=$(docker exec etcd /bin/sh -c "etcdctl member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','") etcd etcdctl endpoint status --write-out table
```
  Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```
  docker exec etcd sh -c "etcdctl endpoint status --endpoints=$(docker exec etcd /bin/sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT member list | cut -d, -f5 | sed -e 's/ //g' | paste -sd ','") --write-out table"
```
  Пример вывода:
  ```
+-----------------+------------------+---------+---------+-----------+-----------+------------+
| ENDPOINT        |        ID        | VERSION | DB SIZE | IS LEADER | RAFT TERM | RAFT INDEX |
+-----------------+------------------+---------+---------+-----------+-----------+------------+
| https://IP:2379 |  e973e4419737125 |  3.2.18 |  553 kB |     false |        32 |    2449410 |
| https://IP:2379 | 4a509c997b26c206 |  3.2.18 |  553 kB |     false |        32 |    2449410 |
| https://IP:2379 | b217e736575e9dd3 |  3.2.18 |  553 kB |      true |        32 |    2449410 |
+-----------------+------------------+---------+---------+-----------+-----------+------------+
  ```
Снять тревогу
Убедившись, что размер DB уменьшился после сжатия и дефрагментации, необходимо отключить аварийный сигнал, чтобы etcd снова разрешил запись.

  Команда:
  ```
docker exec etcd etcdctl alarm list
docker exec etcd etcdctl alarm disarm
docker exec etcd etcdctl alarm list
  ```
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-addressбыла указана при добавлении узла:
  ```
docker exec etcd sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT alarm list"
docker exec etcd sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT alarm disarm"
docker exec etcd sh -c "etcdctl --endpoints=\$ETCDCTL_ENDPOINT alarm list"
  ```
Пример вывода:
  ```
docker exec etcd etcdctl alarm list
memberID:x alarm:NOSPACE
memberID:x alarm:NOSPACE
memberID:x alarm:NOSPACE
docker exec etcd etcdctl alarm disarm
docker exec etcd etcdctl alarm list
  ```
  
## Уровень лога (Log Level)
  
Уровень логирования etcd можно динамически изменять через API. Вы можете настроить отладку логирования, используя приведенные ниже команды.
  
Команда:
  ```
docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl -s -XPUT -d '{"Level":"DEBUG"}' --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) $(docker exec etcd printenv ETCDCTL_ENDPOINTS)/config/local/log
```

  Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```
  docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl -s -XPUT -d '{"Level":"DEBUG"}' --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) $(docker exec etcd printenv ETCDCTL_ENDPOINT)/config/local/log
```
  
Чтобы сбросить уровень журнала до уровня по умолчанию ( INFO), вы можете использовать следующую команду.

  Команда:
  ```
docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl -s -XPUT -d '{"Level":"INFO"}' --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) $(docker exec etcd printenv ETCDCTL_ENDPOINTS)/config/local/log
```
  
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```
  docker run --net=host -v $(docker inspect kubelet --format '{{ range .Mounts }}{{ if eq .Destination "/etc/kubernetes" }}{{ .Source }}{{ end }}{{ end }}')/ssl:/etc/kubernetes/ssl:ro appropriate/curl -s -XPUT -d '{"Level":"INFO"}' --cacert $(docker exec etcd printenv ETCDCTL_CACERT) --cert $(docker exec etcd printenv ETCDCTL_CERT) --key $(docker exec etcd printenv ETCDCTL_KEY) $(docker exec etcd printenv ETCDCTL_ENDPOINT)/config/local/log
```
 ## etcd Контент
  
Если вы хотите исследовать содержимое вашего etcd, вы можете либо просмотреть потоковые события, либо запросить etcd напрямую, см. примеры ниже.
  
## Смотреть потоковые события (Streaming Events)
Команда:
  ```
docker exec etcd etcdctl watch --prefix /registry
  ```
Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
```
  docker exec etcd etcdctl --endpoints=\$ETCDCTL_ENDPOINT watch --prefix /registry
```
Если вы хотите видеть только затронутые ключи (а не двоичные данные), вы можете добавить | grep -a ^/registry к команде для фильтрации только ключей.

  ## Запрос etcd напрямую
Команда:
  ```
docker exec etcd etcdctl get /registry --prefix=true --keys-only
```
  Команда при использовании etcd версии ниже 3.3.x (Kubernetes 1.13.x и ниже) и --internal-address была указана при добавлении узла:
  ```
docker exec etcd etcdctl --endpoints=\$ETCDCTL_ENDPOINT get /registry --prefix=true --keys-only 
```
  
Вы можете обработать данные, чтобы получить сводку по счетчику для каждого ключа, используя следующую команду:
```
  docker exec etcd etcdctl get /registry --prefix=true --keys-only | grep -v ^$ | awk -F'/' '{ if ($3 ~ /cattle.io/) {h[$3"/"$4]++} else { h[$3]++ }} END { for(k in h) print h[k], k }' | sort -nr
```
## Замена неработоспособных нод etcd
  
Когда нода в вашем кластере etcd становится неработоспособным, рекомендуется исправить или удалить отказавшую или неработоспособную ноду перед добавлением новой ноды etcd в кластер.
