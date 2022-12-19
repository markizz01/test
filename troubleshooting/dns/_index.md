Команды/шаги, перечисленные на этой странице, можно использовать для проверки проблем с разрешением имен в вашем кластере.
Убедитесь, что вы настроили правильный kubeconfig (например, export KUBECONFIG=$PWD/kube_config_cluster.yml для Rancher HA) или используете встроенный kubectl через UI (пользовательский интерфейс).
Прежде чем запускать проверки DNS, проверьте [поставщика DNS по умолчанию](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/troubleshooting/dns/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning/rke-clusters/options/#default-dns-provider) для вашего кластера и убедитесь, что [верхний слой сети работает правильно](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/troubleshooting/dns/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/troubleshooting/networking/#check-if-overlay-network-is-functioning-correctly) , так как это также может быть причиной (частично) сбоя разрешения DNS.

**Проверьте, запущены ли модули DNS**
```
kubectl -n kube-system get pods -l k8s-app=kube-dns
```

- **Пример вывода при использовании CoreDNS:**
```
NAME                       READY   STATUS    RESTARTS   AGE
coredns-799dffd9c4-6jhlz   1/1     Running   0          76m
```

- **Пример вывода при использовании kube-dns:**
```
NAME                        READY   STATUS    RESTARTS   AGE
kube-dns-5fd74c7488-h6f7n   3/3     Running   0          4m13s
```

**Проверьте, присутствует ли служба DNS с правильным IP-адресом кластера.**
```
kubectl -n kube-system get svc -l k8s-app=kube-dns
NAME               TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)         AGE
service/kube-dns   ClusterIP   10.43.0.10   <none>        53/UDP,53/TCP   4m13s
```

**Проверьте, разрешаются ли доменные имена**

Проверьте, разрешаются ли внутренние имена кластеров (в этом примере — kubernetes.default), IP-адрес, показанный после Server:, должен совпадать с  IP -адресом CLUSTER-IP службы kube-dns.
```
kubectl run -it --rm --restart=Never busybox --image=busybox:1.28 -- nslookup kubernetes.default
```
- **Пример вывода:**
```
Server:    10.43.0.10
Address 1: 10.43.0.10 kube-dns.kube-system.svc.cluster.local

Name:      kubernetes.default
Address 1: 10.43.0.1 kubernetes.default.svc.cluster.local
pod "busybox" deleted
```

Проверьте, разрешаются ли внешние имена (в этом примере www.google.com)
kubectl run -it --rm --restart=Never busybox --image=busybox:1.28 -- nslookup www.google.com

- **Пример вывода:**
```
Server:    10.43.0.10
Address 1: 10.43.0.10 kube-dns.kube-system.svc.cluster.local

Name:      www.google.com
Address 1: 2a00:1450:4009:80b::2004 lhr35s04-in-x04.1e100.net
Address 2: 216.58.211.100 ams15s32-in-f4.1e100.net
pod "busybox" deleted
```

Если вы хотите проверить разрешение доменных имен на всех хостах, выполните следующие действия:

1.	Сохраните следующий файл какds-dnstest.yml
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: dnstest
spec:
  selector:
      matchLabels:
        name: dnstest
  template:
    metadata:
      labels:
        name: dnstest
    spec:
      tolerations:
      - operator: Exists
      containers:
      - image: busybox:1.28
        imagePullPolicy: Always
        name: alpine
        command: ["sh", "-c", "tail -f /dev/null"]
        terminationMessagePath: /dev/termination-log
```
2.	Запустите его с помощью kubectl create -f ds-dnstest.yml
3.	Дождитесь пока kubectl rollout status ds/dnstest –w вернется: daemon set "dnstest" successfully rolled out.
4.	Настройте переменную DOMAIN на полное доменное имя (FQDN), которое хост должен иметь возможность разрешать ( www.google.com используется в качестве примера), и выполните следующую команду, чтобы позволить каждому контейнеру на каждом хосте разрешать настроенное доменное имя (это одна строка команда).
```
export DOMAIN=www.google.com; echo "=> Start DNS resolve test"; kubectl get pods -l name=dnstest --no-headers -o custom-columns=NAME:.metadata.name,HOSTIP:.status.hostIP | while read pod host; do kubectl exec $pod -- /bin/sh -c "nslookup $DOMAIN > /dev/null 2>&1"; RC=$?; if [ $RC -ne 0 ]; then echo $host cannot resolve $DOMAIN; fi; done; echo "=> End DNS resolve test"
```
5.	Когда эта команда завершит выполнение, вывод, указывающий, что все правильно:
```
=> Start DNS resolve test
=> End DNS resolve test
```

Если вы видите ошибку в выводе, это означает, что указанные хосты не могут разрешить данное полное доменное имя.

Пример вывода ошибки в ситуации, когда хост с IP 209.97.182.150 заблокировал порты UDP.
```
=> Start DNS resolve test
command terminated with exit code 1
209.97.182.150 cannot resolve www.google.com
=> End DNS resolve test
```

Очистите alpine DaemonSet, запустив kubectl delete ds/dnstest.

# Специфика CoreDNS

**Проверьте ведение журнала CoreDNS**
```
kubectl -n kube-system logs -l k8s-app=kube-dns
```

**Проверьте конфигурацию**

Конфигурация CoreDNS хранится в configmap пространстве coredns в kube-system 
```
kubectl -n kube-system get configmap coredns -o go-template={{.data.Corefile}}
```

**Проверьте вышестоящие серверы имен в resolv.conf**

По умолчанию настроенные серверы имен на узле (в /etc/resolv.conf) будут использоваться в качестве вышестоящих серверов имен для CoreDNS. Вы можете проверить этот файл на хосте или запустить следующий модуль dnsPolicy с установленным значением Default, который унаследует /etc/resolv.confот хоста, на котором он работает.
```
kubectl run -i --restart=Never --rm test-${RANDOM} --image=ubuntu --overrides='{"kind":"Pod", "apiVersion":"v1", "spec": {"dnsPolicy":"Default"}}' -- sh -c 'cat /etc/resolv.conf'
```

**Включить ведение журнала запросов**

Включить ведение журнала запросов можно, включив [плагин журнала](https://coredns.io/plugins/log/) в конфигурации Corefile в configmap coredns. Вы можете сделать это, используя kubectl -n kube-system edit configmap coredns или используя приведенную ниже команду, чтобы заменить конфигурацию на месте:
```
kubectl get configmap -n kube-system coredns -o json | sed -e 's_loadbalance_log\\n    loadbalance_g' | kubectl apply -f –
```

Все запросы теперь будут регистрироваться и могут быть проверены с помощью команды в [Check CoreDNS logging .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/troubleshooting/dns/_index.md)

# Специфика kube-dns

**Проверьте вышестоящие серверы имен в контейнере kubedns.**

По умолчанию настроенные серверы имен на хосте (в /etc/resolv.conf) будут использоваться в качестве вышестоящих серверов имен для kube-dns. Иногда хост запускает локальный кэширующий DNS-сервер имен, что означает, что адрес в /etc/resolv.conf будет указывать на адрес в диапазоне обратной связи ( 127.0.0.0/8), который будет недоступен для контейнера. В случае Ubuntu 18.04 это делается с помощью systemd-resolved. Мы определяем systemd-resolved, работает ли он, и автоматически используем файл /etc/resolv.conf с правильными вышестоящими серверами имен (которые расположены по адресу /run/systemd/resolve/resolv.conf).
Используйте следующую команду, чтобы проверить вышестоящие серверы имен, используемые контейнером kubedns:
```
kubectl -n kube-system get pods -l k8s-app=kube-dns --no-headers -o custom-columns=NAME:.metadata.name,HOSTIP:.status.hostIP | while read pod host; do echo "Pod ${pod} on host ${host}"; kubectl -n kube-system exec $pod -c kubedns cat /etc/resolv.conf; done
```

Пример вывода:
```
Pod kube-dns-667c7cb9dd-z4dsf on host x.x.x.x
nameserver 1.1.1.1
nameserver 8.8.4.4
```

Если вывод показывает адрес в диапазоне обратной связи ( 127.0.0.0/8), вы можете исправить это двумя способами:
-	Убедитесь, что на ваших нодах в кластере указаны правильные серверы имен /etc/resolv.conf. Чтобы узнать, как это сделать, обратитесь к документации по вашей операционной системе. Убедитесь, что вы выполнили это перед инициализацией кластера, или перезагрузите ноды после внесения изменений.
-	Настройте kubelet для использования другого файла для разрешения имен, extra_args как показано ниже (где файл /run/resolvconf/resolv.conf находится с правильными серверами имен):
```
services:
  kubelet:
    extra_args:
      resolv-conf: "/run/resolvconf/resolv.conf"
```
***Примечание.** Поскольку приложение kubelet выполняется внутри контейнера, путь к файлам, расположенным /etc и /usr находящимся в /host/etc и /host/usr , так же проходит внутри контейнера  kubelet*

См. [Редактирование кластера как YAML](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/troubleshooting/dns/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-admin/editing-clusters/#editing-clusters-with-yaml) , как применить это изменение. Когда подготовка кластера завершена, вам необходимо удалить модуль kube-dns, чтобы активировать новый параметр в модуле:
```
kubectl delete pods -n kube-system -l k8s-app=kube-dns
pod "kube-dns-5fd74c7488-6pwsf" deleted
```

Попробуйте еще раз разрешить имя с помощью [команды «Проверить, разрешаются ли доменные имена»](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/troubleshooting/dns/_index.md#check-if-domain-names-are-resolving) . (Check if domain names are resolving).

Если вы хотите проверить конфигурацию kube-dns в своем кластере (например, чтобы проверить, настроены ли другие вышестоящие серверы имен), вы можете выполнить следующую команду, чтобы просмотреть конфигурацию kube-dns:
```
kubectl -n kube-system get configmap kube-dns -o go-template='{{range $key, $value := .data}}{{ $key }}{{":"}}{{ $value }}{{"\n"}}{{end}}'
```

Пример вывода:
```
upstreamNameservers:["1.1.1.1"]
```
