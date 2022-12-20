# Справочник по выражениям PromQL

Выражения PromQL в этом документе можно использовать для настройки предупреждений.

Дополнительные сведения о запросах к базе данных временных рядов Prometheus см. в официальной [документации Prometheus.](https://prometheus.io/docs/prometheus/latest/querying/basics/)

-	Метрики кластера
    -	Загрузка ЦП кластера
    -	Средняя нагрузка кластера
    -	Использование памяти кластера
    -	Использование кластерного диска
    -	Дисковый ввод-вывод кластера
    -	Сетевые пакеты кластера
    -	Кластерный сетевой ввод-вывод
-	Метрики узла
    -	Загрузка ЦП узла
    -	Средняя нагрузка узла
    -	Использование памяти узла
    -	Использование диска узла
    -	Дисковый ввод-вывод узла
    -	Сетевые пакеты узла
    -	Сетевой ввод-вывод узла
-	И т. д. Метрики
    -	Ecd имеет лидера
    -	Количество смен лидера
    -	Количество неудачных предложений
    -	Клиентский трафик GRPC
    -	Одноранговый трафик
    -	Размер БД
    -	Активные потоки
    -	Предложения плота
    -	Скорость RPC
    -	Дисковые операции
    -	Продолжительность синхронизации диска
-	Метрики компонентов Kubernetes
    -	Задержка запроса сервера API
    -	Частота запросов к серверу API
    -	Планирование неудачных модулей
    -	Глубина очереди диспетчера контроллеров
    -	Задержка планировщика E2E
    -	Попытки вытеснения планировщика
    -	Соединения контроллера входящего трафика
    -	Время обработки запроса контроллера входящего трафика
-	Метрики ведения журнала Rancher
    -	Частота буферной очереди Fluentd
    -	Свободная скорость ввода
    -	Коэффициент ошибок вывода Fluentd
    -	Скорость вывода Fluentd
-	Показатели рабочей нагрузки
    -	Загрузка ЦП рабочей нагрузки
    -	Использование памяти рабочей нагрузки
    -	Сетевые пакеты рабочей нагрузки
    -	Сетевой ввод-вывод рабочей нагрузки
    -	Дисковый ввод-вывод рабочей нагрузки
-	Метрики пода
    -	Загрузка ЦП пода
    -	Использование памяти модуля
    -	Сетевые пакеты Pod
    -	Сетевой ввод-вывод модуля
    -	Дисковый ввод-вывод модуля
-	Метрики контейнера
    -	Использование ЦП контейнера
    -	Использование памяти контейнера
    -	Дисковый ввод-вывод контейнера

# Метрики кластера
## Загрузка CPU кластера

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|1 - (avg(irate(node\_cpu\_seconds\_total{mode="idle"}[5m])) by (instance))|
|Резюме|1 - (avg(irate(node\_cpu\_seconds\_total{mode="idle"}[5m])))|

## Средняя нагрузка кластера

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|
|нагрузка1|sum(node\_load1) by (instance) / count(node\_cpu\_seconds\_total{mode="system"}) by (instance)|
|нагрузка5|sum(node\_load5) by (instance) / count(node\_cpu\_seconds\_total{mode="system"}) by (instance)|
|нагрузка15|sum(node\_load15) by (instance) / count(node\_cpu\_seconds\_total{mode="system"}) by (instance)||
|Резюме|
|нагрузка1|sum(node\_load1) by (instance) / count(node\_cpu\_seconds\_total{mode="system"})|
|нагрузка5|sum(node\_load5) by (instance) / count(node\_cpu\_seconds\_total{mode="system"})|
|нагрузка15|sum(node\_load15) by (instance) / count(node\_cpu\_seconds\_total{mode="system"})||


## Использование памяти кластера

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|1 - sum(node\_memory\_MemAvailable\_bytes) by (instance) / sum(node\_memory\_MemTotal\_bytes) by (instance)|
|Резюме|1 - sum(node\_memory\_MemAvailable\_bytes) / sum(node\_memory\_MemTotal\_bytes)|

## Использование Cluster Disk

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|(sum(node\_filesystem\_size\_bytes{device!="rootfs"}) by (instance) - sum(node\_filesystem\_free\_bytes{device!="rootfs"}) by (instance)) / sum(node\_filesystem\_size\_bytes{device!="rootfs"}) by (instance)|
|Резюме|(sum(node\_filesystem\_size\_bytes{device!="rootfs"}) - sum(node\_filesystem\_free\_bytes{device!="rootfs"})) / sum(node\_filesystem\_size\_bytes{device!="rootfs"})|

## Дисковый ввод-вывод кластера (Cluster Disk I/O)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||читать|sum(rate(node\_disk\_read\_bytes\_total[5m])) by (instance)|
|написано|sum(rate(node\_disk\_written\_bytes\_total[5m])) by (instance)||
|Резюме||читать|sum(rate(node\_disk\_read\_bytes\_total[5m]))|
|написано|sum(rate(node\_disk\_written\_bytes\_total[5m]))||

## Сетевые пакеты кластера Cluster Network Packets

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||получить-выпало|sum(rate(node\_network\_receive\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)|
|прием-ошибки|sum(rate(node\_network\_receive\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|получить-пакеты|sum(rate(node\_network\_receive\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|передача сбрасывается|sum(rate(node\_network\_transmit\_drop\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|ошибки передачи|sum(rate(node\_network\_transmit\_errs\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|передавать-пакеты|sum(rate(node\_network\_transmit\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)||
|Резюме||получить-выпало|sum(rate(node\_network\_receive\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))|
|прием-ошибки|sum(rate(node\_network\_receive\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|получить-пакеты|sum(rate(node\_network\_receive\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|передача сбрасывается|sum(rate(node\_network\_transmit\_drop\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|ошибки передачи|sum(rate(node\_network\_transmit\_errs\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|передавать-пакеты|sum(rate(node\_network\_transmit\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))||

## Cluster Network I/O

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||Получать|sum(rate(node\_network\_receive\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)|
|передавать|sum(rate(node\_network\_transmit\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)||
|Резюме||Получать|sum(rate(node\_network\_receive\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))|
|передавать|sum(rate(node\_network\_transmit\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))||

# Метрики Node Metrics
## Загрузка Node CPU

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|avg(irate(node\_cpu\_seconds\_total{mode!="idle", instance=~"$instance"}[5m])) by (mode)|
|Резюме|1 - (avg(irate(node\_cpu\_seconds\_total{mode="idle", instance=~"$instance"}[5m])))|

## Средняя нагрузка узла(Node)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||нагрузка1|sum(node\_load1{instance=~"$instance"}) / count(node\_cpu\_seconds\_total{mode="system",instance=~"$instance"})|
|нагрузка5|sum(node\_load5{instance=~"$instance"}) / count(node\_cpu\_seconds\_total{mode="system",instance=~"$instance"})|
|нагрузка15|sum(node\_load15{instance=~"$instance"}) / count(node\_cpu\_seconds\_total{mode="system",instance=~"$instance"})||
|Резюме||нагрузка1|sum(node\_load1{instance=~"$instance"}) / count(node\_cpu\_seconds\_total{mode="system",instance=~"$instance"})|
|нагрузка5|sum(node\_load5{instance=~"$instance"}) / count(node\_cpu\_seconds\_total{mode="system",instance=~"$instance"})|
|нагрузка15|sum(node\_load15{instance=~"$instance"}) / count(node\_cpu\_seconds\_total{mode="system",instance=~"$instance"})||

## Использование памяти узла

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|1 - sum(node\_memory\_MemAvailable\_bytes{instance=~"$instance"}) / sum(node\_memory\_MemTotal\_bytes{instance=~"$instance"})|
|Резюме|1 - sum(node\_memory\_MemAvailable\_bytes{instance=~"$instance"}) / sum(node\_memory\_MemTotal\_bytes{instance=~"$instance"})|

## Использование диска узла

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|(sum(node\_filesystem\_size\_bytes{device!="rootfs",instance=~"$instance"}) by (device) - sum(node\_filesystem\_free\_bytes{device!="rootfs",instance=~"$instance"}) by (device)) / sum(node\_filesystem\_size\_bytes{device!="rootfs",instance=~"$instance"}) by (device)|
|Резюме|(sum(node\_filesystem\_size\_bytes{device!="rootfs",instance=~"$instance"}) - sum(node\_filesystem\_free\_bytes{device!="rootfs",instance=~"$instance"})) / sum(node\_filesystem\_size\_bytes{device!="rootfs",instance=~"$instance"})|

## Node Disk I/O

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||читать|sum(rate(node\_disk\_read\_bytes\_total{instance=~"$instance"}[5m]))|
|написано|sum(rate(node\_disk\_written\_bytes\_total{instance=~"$instance"}[5m]))||
|Резюме||читать|sum(rate(node\_disk\_read\_bytes\_total{instance=~"$instance"}[5m]))|
|написано|sum(rate(node\_disk\_written\_bytes\_total{instance=~"$instance"}[5m]))||

## Сетевые пакеты узла

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||получить-выпало|sum(rate(node\_network\_receive\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)|
|прием-ошибки|sum(rate(node\_network\_receive\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)|
|получить-пакеты|sum(rate(node\_network\_receive\_packets\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)|
|передача сбрасывается|sum(rate(node\_network\_transmit\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)|
|ошибки передачи|sum(rate(node\_network\_transmit\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)|
|передавать-пакеты|sum(rate(node\_network\_transmit\_packets\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)||
|Резюме||получить-выпало|sum(rate(node\_network\_receive\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))|
|прием-ошибки|sum(rate(node\_network\_receive\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))|
|получить-пакеты|sum(rate(node\_network\_receive\_packets\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))|
|передача сбрасывается|sum(rate(node\_network\_transmit\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))|
|ошибки передачи|sum(rate(node\_network\_transmit\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))|
|передавать-пакеты|sum(rate(node\_network\_transmit\_packets\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))||

## Node Network I/O

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||Получать|sum(rate(node\_network\_receive\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)|
|передавать|sum(rate(node\_network\_transmit\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m])) by (device)||
|Резюме||Получать|sum(rate(node\_network\_receive\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))|
|передавать|sum(rate(node\_network\_transmit\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*",instance="$instance"}[5m]))||

# Etcd  Метрики

## Etcd имеет лидера
```
max(etcd\_server\_has\_leader)
```
## Количество смен лидера
```
max(etcd\_server\_leader\_changes\_seen\_total)
```
## Количество неудачных предложений
```
sum(etcd\_server\_proposals\_failed\_total)
```
## Клиентский трафик GRPC

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||в (in)|sum(rate(etcd\_network\_client\_grpc\_received\_bytes\_total[5m])) by (instance)|
|вне (out)|sum(rate(etcd\_network\_client\_grpc\_sent\_bytes\_total[5m])) by (instance)||
|Резюме||в|sum(rate(etcd\_network\_client\_grpc\_received\_bytes\_total[5m]))|
|вне|sum(rate(etcd\_network\_client\_grpc\_sent\_bytes\_total[5m]))||

## Одноранговый трафик

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||в|sum(rate(etcd\_network\_peer\_received\_bytes\_total[5m])) by (instance)|
|вне|sum(rate(etcd\_network\_peer\_sent\_bytes\_total[5m])) by (instance)||
|Резюме||в|sum(rate(etcd\_network\_peer\_received\_bytes\_total[5m]))|
|вне|sum(rate(etcd\_network\_peer\_sent\_bytes\_total[5m]))||

## Размер DB

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|sum(etcd\_debugging\_mvcc\_db\_total\_size\_in\_bytes) by (instance)|
|Резюме|sum(etcd\_debugging\_mvcc\_db\_total\_size\_in\_bytes)|

## Активные потоки

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||Время аренды| | |sum(grpc\_server\_started\_total{grpc\_service="etcdserverpb.Lease",grpc\_type="bidi\_stream"}) by (instance) - sum(grpc\_server\_handled\_total{grpc\_service="etcdserverpb.Lease",grpc\_type="bidi\_stream"}) by (instance)|
|смотреть| | |sum(grpc\_server\_started\_total{grpc\_service="etcdserverpb.Watch",grpc\_type="bidi\_stream"}) by (instance) - sum(grpc\_server\_handled\_total{grpc\_service="etcdserverpb.Watch",grpc\_type="bidi\_stream"}) by (instance)||
|Резюме||Время аренды|sum(grpc\_server\_started\_total{grpc\_service="etcdserverpb.Lease",grpc\_type="bidi\_stream"}) - sum(grpc\_server\_handled\_total{grpc\_service="etcdserverpb.Lease",grpc\_type="bidi\_stream"})|
|смотреть|sum(grpc\_server\_started\_total{grpc\_service="etcdserverpb.Watch",grpc\_type="bidi\_stream"}) - sum(grpc\_server\_handled\_total{grpc\_service="etcdserverpb.Watch",grpc\_type="bidi\_stream"})||

## Предложения Raft

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||примененный|sum(increase(etcd\_server\_proposals\_applied\_total[5m])) by (instance)|
|переданный |sum(increase(etcd\_server\_proposals\_committed\_total[5m])) by (instance)|
|ожидаемый|sum(increase(etcd\_server\_proposals\_pending[5m])) by (instance)|
|неудавшийся|sum(increase(etcd\_server\_proposals\_failed\_total[5m])) by (instance)||
|Резюме||примененный|sum(increase(etcd\_server\_proposals\_applied\_total[5m]))|
|переданный |sum(increase(etcd\_server\_proposals\_committed\_total[5m]))|
|ожидаемый|sum(increase(etcd\_server\_proposals\_pending[5m]))|
|неудавшийся|sum(increase(etcd\_server\_proposals\_failed\_total[5m]))||

## коэффициент RPC (RPC Rate)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||total|sum(rate(grpc\_server\_started\_total{grpc\_type="unary"}[5m])) by (instance)|
|fail|sum(rate(grpc\_server\_handled\_total{grpc\_type="unary",grpc\_code!="OK"}[5m])) by (instance)||
|Резюме||total|sum(rate(grpc\_server\_started\_total{grpc\_type="unary"}[5m]))|
|fail|sum(rate(grpc\_server\_handled\_total{grpc\_type="unary",grpc\_code!="OK"}[5m]))||

## Операции с диском

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||commit-called-by-backend|sum(rate(etcd\_disk\_backend\_commit\_duration\_seconds\_sum[1m])) by (instance)|
|fsync-called-by-wal|sum(rate(etcd\_disk\_wal\_fsync\_duration\_seconds\_sum[1m])) by (instance)||
|Резюме||commit-called-by-backend|sum(rate(etcd\_disk\_backend\_commit\_duration\_seconds\_sum[1m]))|
|fsync-called-by-wal|sum(rate(etcd\_disk\_wal\_fsync\_duration\_seconds\_sum[1m]))||

## Продолжительность Disk Sync

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||wal|histogram\_quantile(0.99, sum(rate(etcd\_disk\_wal\_fsync\_duration\_seconds\_bucket[5m])) by (instance, le))|
|db|histogram\_quantile(0.99, sum(rate(etcd\_disk\_backend\_commit\_duration\_seconds\_bucket[5m])) by (instance, le))||
|Резюме||wal|sum(histogram\_quantile(0.99, sum(rate(etcd\_disk\_wal\_fsync\_duration\_seconds\_bucket[5m])) by (instance, le)))|
|db|sum(histogram\_quantile(0.99, sum(rate(etcd\_disk\_backend\_commit\_duration\_seconds\_bucket[5m])) by (instance, le)))||

# Метрики компонентов Kubernetes

## Задержка запроса сервера API

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|avg(apiserver\_request\_latencies\_sum / apiserver\_request\_latencies\_count) by (instance, verb) /1e+06|
|Резюме|avg(apiserver\_request\_latencies\_sum / apiserver\_request\_latencies\_count) by (instance) /1e+06|

## Частота запросов к серверу API

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|sum(rate(apiserver\_request\_count[5m])) by (instance, code)|
|Резюме|sum(rate(apiserver\_request\_count[5m])) by (instance)|

## Диспетчеризация неудачных (Failed) Pods

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|sum(kube\_pod\_status\_scheduled{condition="false"})|
|Резюме|sum(kube\_pod\_status\_scheduled{condition="false"})|

## Глубина диспетчера контроллеров очереди (Queue)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||volumes|sum(volumes\_depth) by instance|
|deployment|sum(deployment\_depth) by instance|
|replicaset|sum(replicaset\_depth) by instance|
|service|sum(service\_depth) by instance|
|serviceaccount|sum(serviceaccount\_depth) by instance|
|endpoint|sum(endpoint\_depth) by instance|
|daemonset|sum(daemonset\_depth) by instance|
|statefulset|sum(statefulset\_depth) by instance|
|replicationmanager|sum(replicationmanager\_depth) by instance||
|Резюме||volumes|sum(volumes\_depth)|
|deployment|sum(deployment\_depth)|
|replicaset|sum(replicaset\_depth)|
|service|sum(service\_depth)|
|serviceaccount|sum(serviceaccount\_depth)|
|endpoint|sum(endpoint\_depth)|
|daemonset|sum(daemonset\_depth)|
|statefulset|sum(statefulset\_depth)|
|replicationmanager|sum(replicationmanager\_depth)||

## Задержка (время ожидания) планировщика E2E (Scheduler E2E Scheduling)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|histogram\_quantile(0.99, sum(scheduler\_e2e\_scheduling\_latency\_microseconds\_bucket) by (le, instance)) / 1e+06|
|Резюме|sum(histogram\_quantile(0.99, sum(scheduler\_e2e\_scheduling\_latency\_microseconds\_bucket) by (le, instance)) / 1e+06)|

## Попытки вытеснения планировщика (Scheduler)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|sum(rate(scheduler\_total\_preemption\_attempts[5m])) by (instance)|
|Резюме|sum(rate(scheduler\_total\_preemption\_attempts[5m]))|

## Подключение контроллера входа (Ingress Controller)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||читаемый|sum(nginx\_ingress\_controller\_nginx\_process\_connections{state="reading"}) by (instance)|
|ожидаемый|sum(nginx\_ingress\_controller\_nginx\_process\_connections{state="waiting"}) by (instance)|
|написанный|sum(nginx\_ingress\_controller\_nginx\_process\_connections{state="writing"}) by (instance)|
|принятый|sum(ceil(increase(nginx\_ingress\_controller\_nginx\_process\_connections\_total{state="accepted"}[5m]))) by (instance)|
|активированный|sum(ceil(increase(nginx\_ingress\_controller\_nginx\_process\_connections\_total{state="active"}[5m]))) by (instance)|
|обрабатывемый|sum(ceil(increase(nginx\_ingress\_controller\_nginx\_process\_connections\_total{state="handled"}[5m]))) by (instance)||
|Резюме||читаемый|sum(nginx\_ingress\_controller\_nginx\_process\_connections{state="reading"})|
|ожидаемый|sum(nginx\_ingress\_controller\_nginx\_process\_connections{state="waiting"})|
|написанный|sum(nginx\_ingress\_controller\_nginx\_process\_connections{state="writing"})|
|принятый|sum(ceil(increase(nginx\_ingress\_controller\_nginx\_process\_connections\_total{state="accepted"}[5m])))|
|активированный|sum(ceil(increase(nginx\_ingress\_controller\_nginx\_process\_connections\_total{state="active"}[5m])))|
|обрабатываемый|sum(ceil(increase(nginx\_ingress\_controller\_nginx\_process\_connections\_total{state="handled"}[5m])))||

