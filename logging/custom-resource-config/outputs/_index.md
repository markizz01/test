Для получения полной информации о настройке Outputs и ClusterOutputs см . документацию оператора Banzai Cloud Logging   (https://banzaicloud.com/docs/one-eye/logging-operator/configuration/output/). 

+	Конфигурация
+	YAML-примеры
    -	Вывод кластера в ElasticSearch
    -	Вывод в Splunk
    -	Вывод в системный журнал
    -	Неподдерживаемые выходы

#Конфигурация
##Выходы

Ресурс Output определяет, куда ваш Flows может отправлять сообщения журнала. Outputs является завершающим этапом регистрации Flow.

Output-ресурс с пространством имен, что означает, что только тот Flow может получить доступ к нему, который находится в том же пространстве имен.

Вы можете использовать секреты (secrets) в этих определениях, но они также должны находиться в одном и том же пространстве имен.

Outputs можно настроить, заполнив формы в пользовательском интерфейсе Rancher.

Дополнительные сведения о пользовательском ресурсе Output см . в разделе OutputSpec. https://banzaicloud.com/docs/one-eye/logging-operator/configuration/crds/v1beta1/output_types/

Пользовательский интерфейс Rancher предоставляет формы для настройки следующих типов  Output:

-	Amazon ElasticSearch
-	Хранилище Azure
-	Облачный дозор
-	датадог
-	Эластичный поиск
-	Файл
-	свободно
-	ГКС
-	Кафка
-	Кинезис Стрим
-	ЛогДНК
-	ЛогZ
-	Локи
-	Новая реликвия
-	Splunk
-	СумоЛогик
-	системный журнал

Пользовательский интерфейс Rancher предоставляет формы для настройки типа Output, цели и учетные данные доступа, если это применимо.

Пример конфигурации для каждого подключаемого модуля ведения журнала, поддерживаемого оператором ведения журнала, см. в документации оператора ведения журнала. https://banzaicloud.com/docs/one-eye/logging-operator/configuration/plugins/outputs/

## Выходы кластера

ClusterOutput определяет Output без ограничений пространства имен. Он эффективен только при развертывании в том же пространстве имен, что и оператор ведения журнала.

ClusterOutputs можно настроить, заполнив формы в пользовательском интерфейсе Rancher.

Дополнительные сведения о  пользовательском ресурсе ClusterOutput см . в разделе ClusterOutput. https://banzaicloud.com/docs/one-eye/logging-operator/configuration/crds/v1beta1/clusteroutput_types/ 

# YAML-примеры

После установки ведения журнала вы можете использовать эти примеры для создания собственного канала ведения журнала.

-	Вывод кластера в ElasticSearch
-	Вывод в Splunk
-	Вывод в системный журнал
-	Неподдерживаемые выходы

## Вывод кластера в ElasticSearch

Допустим, вы хотите отправить все журналы в своем кластере в elasticsearch кластер. Сначала мы создаем кластер Output.

```
apiVersion: logging.banzaicloud.io/v1beta1
kind: ClusterOutput
metadata:
    name: "example-es"
    namespace: "cattle-logging-system"
spec:
    elasticsearch:
      host: elasticsearch.example.com
      port: 9200
      scheme: http
```      
      
Мы создали ClusterOutput без настройки elasticsearch в том же пространстве имен, что и наш оператор: cattle-logging-system.. Каждый раз, когда мы создаем ClusterFlow или ClusterOutput, мы должны поместить его в пространство имен  cattle-logging-system.

Теперь, когда мы настроили то, где мы хотим вести журналы, давайте настроим все журналы так, чтобы они направлялись в этот ClusterOutput.

```
apiVersion: logging.banzaicloud.io/v1beta1
kind: ClusterFlow
metadata:
    name: "all-logs"
    namespace: "cattle-logging-system"
spec:
  globalOutputRefs:
    - "example-es"    
```

Теперь мы должны увидеть наш настроенный индекс с журналами в нем.

## Вывод в Splunk

Что, если у нас есть группа приложений, которая хочет, чтобы журналы из определенных пространств имен отправлялись только на splunk сервер? В этом случае мы можем использовать пространство имен Outputs и Flows.

Прежде чем мы начнем, давайте настроим приложение этой команды: coolapp.

```
apiVersion: v1
kind: Namespace
metadata:
  name: devteam
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: coolapp
  namespace: devteam
  labels:
    app: coolapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: coolapp
  template:
    metadata:
      labels:
        app: coolapp
    spec:
      containers:
        - name: generator
          image: paynejacob/loggenerator:latest
```          
          
При coolapp запуске мы будем следовать по тому же пути, что и при создании файла ClusterOutput. Однако, в отличие от ClusterOutputs, мы создаем наши Output в в  нашем приложении.

```
apiVersion: logging.banzaicloud.io/v1beta1
kind: Output
metadata:
  name: "devteam-splunk"
  namespace: "devteam"
spec:
  splunkHec:
    hec_host: splunk.example.com
    hec_port: 8088
    protocol: http
```

Еще раз, давайте дополним наши Output журналы:

```
apiVersion: logging.banzaicloud.io/v1beta1
kind: Flow
metadata:
  name: "devteam-logs"
  namespace: "devteam"
spec:
  localOutputRefs:
    - "devteam-splunk"
```    
    
## Вывод в системный журнал

Допустим, вы хотите отправить все журналы в своем кластере на syslog сервер. Сначала мы создаем ClusterOutput:

```
apiVersion: logging.banzaicloud.io/v1beta1
kind: ClusterOutput
metadata:
  name: "example-syslog"
  namespace: "cattle-logging-system"
spec:
  syslog:
    buffer:
      timekey: 30s
      timekey_use_utc: true
      timekey_wait: 10s
      flush_interval: 5s
    format:
      type: json
      app_name_field: test
    host: syslog.example.com
    insecure: true
    port: 514
    transport: tcp
```

Теперь, когда мы настроили то, куда мы хотим отправить журналы, давайте настроим все журналы так, чтобы они направлялись в Output.

```
apiVersion: logging.banzaicloud.io/v1beta1
kind: ClusterFlow
metadata:
  name: "all-logs"
  namespace: cattle-logging-system
spec:
  globalOutputRefs:
    - "example-syslog"
```

## Неподдерживаемые выходы

В последнем примере мы создаем объект Output  для записи журналов в место назначения, которое не поддерживается по умолчанию:

**Примечание о системном журнале syslog** — это поддерживаемый файл Output. Однако в этом примере по-прежнему содержится обзор использования неподдерживаемых подключаемых модулей.

```
apiVersion: v1
kind: Secret
metadata:
  name: syslog-config
  namespace: cattle-logging-system
type: Opaque
stringData:
  fluent-bit.conf: |
    [INPUT]
        Name              forward
        Port              24224

    [OUTPUT]
        Name              syslog
        InstanceName      syslog-output
        Match             *
        Addr              syslog.example.com
        Port              514
        Cluster           ranchers

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: fluentbit-syslog-forwarder
  namespace: cattle-logging-system
  labels:
    output: syslog
spec:
  selector:
    matchLabels:
      output: syslog
  template:
    metadata:
      labels:
        output: syslog
    spec:
      containers:
      - name: fluentbit
        image: paynejacob/fluent-bit-out-syslog:latest
        ports:
          - containerPort: 24224
        volumeMounts:
          - mountPath: "/fluent-bit/etc/"
            name: configuration
      volumes:
      - name: configuration
        secret:
          secretName: syslog-config
---
apiVersion: v1
kind: Service
metadata:
  name: syslog-forwarder
  namespace: cattle-logging-system
spec:
  selector:
    output: syslog
  ports:
    - protocol: TCP
      port: 24224
      targetPort: 24224
---
apiVersion: logging.banzaicloud.io/v1beta1
kind: ClusterFlow
metadata:
  name: all-logs
  namespace: cattle-logging-system
spec:
  globalOutputRefs:
    - syslog
---
apiVersion: logging.banzaicloud.io/v1beta1
kind: ClusterOutput
metadata:
  name: syslog
  namespace: cattle-logging-system
spec:
  forward:
    servers:
      - host: "syslog-forwarder.cattle-logging-system"
    require_ack_response: false
    ignore_network_errors_at_startup: false
```   
    
Давайте разберем, что здесь происходит. Во-первых, мы создаем развертывание контейнера с дополнительным подключаемым модулем syslog, который принимает журналы, пересылаемые из другого fluentd. Затем мы создаем настроенный сервер пересылки Output для нашего развертывания контейнера. После этого развернутый fluentd перенаправит все журналы в настроенное syslog место назначения.

