Для получения полной информации о настройке **Flows** и **ClusterFlows** см . документацию оператора Banzai Cloud Logging. https://banzaicloud.com/docs/one-eye/logging-operator/configuration/flow/

**Конфигурация**
+	[**Потоки**](https://github.com/markizz01/test/blob/main/logging/custom-resource-config/flows/_index.md#%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B8)
    - [**Соответствия**](https://github.com/markizz01/test/blob/main/logging/custom-resource-config/flows/_index.md#%D1%81%D0%BE%D0%BE%D1%82%D0%B2%D0%B5%D1%82%D1%81%D1%82%D0%B2%D0%B8%D1%8F-matchs---%D0%BC%D0%B0%D1%82%D1%87%D0%B8)
    -	[**Фильтры**](https://github.com/markizz01/test/blob/main/logging/custom-resource-config/flows/_index.md#%D1%84%D0%B8%D0%BB%D1%8C%D1%82%D1%80%D1%8B)
    -	[**Выходы**](https://github.com/markizz01/test/blob/main/logging/custom-resource-config/flows/_index.md#%D0%B2%D1%8B%D1%85%D0%BE%D0%B4%D1%8B)
+	[**Кластерные потоки**](https://github.com/markizz01/test/blob/main/logging/custom-resource-config/flows/_index.md#%D0%BA%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%BD%D1%8B%D0%B5-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B8)

# Потоки

A **Flow** определяет, какие журналы собирать и фильтровать и на какой выход отправлять журналы.

Это **Flow** ресурс с пространством имен, что означает, что журналы будут собираться только из пространства имен, в котором **Flow** развернут.
Flows можно настроить, заполнив формы в пользовательском интерфейсе Rancher.

Дополнительные сведения о Flow - пользовательском ресурсе см . в разделе FlowSpec  (https://banzaicloud.com/docs/one-eye/logging-operator/configuration/crds/v1beta1/flow_types/) .

## Соответствия (matchs) - матчи

Операторы соответствия используются для выбора контейнеров, из которых следует извлекать журналы.

Вы можете указать операторы соответствия, чтобы выбрать или исключить журналы в соответствии с метками Kubernetes, именами контейнеров и хостов. Операторы соответствия оцениваются в том порядке, в котором они определены, и обрабатываются только до тех пор, пока не будет применено первое соответствующее правило выбора или исключения.

Матчи можно настроить, заполнив Flow или ClusterFlow формы в пользовательском интерфейсе Rancher.
Подробные примеры использования оператора match см. в официальной документации по маршрутизации журналов (https://banzaicloud.com/docs/one-eye/logging-operator/configuration/log-routing/).

## Фильтры

Вы можете определить один или несколько фильтров в файле Flow. Фильтры могут выполнять различные действия с журналами, например, добавлять дополнительные данные, преобразовывать журналы или анализировать значения из записей. Фильтры Flow применяются в порядке определения.
Список фильтров, поддерживаемых оператором Banzai Cloud Logging, см . на этой странице  (https://banzaicloud.com/docs/one-eye/logging-operator/configuration/plugins/filters/).

Фильтры необходимо настроить в YAML.

## Выходы

Output будет получать журналы из Flow. Поскольку Flow - это ресурс с пространством имен, то  Output должен находиться в том же пространстве имен, что и файл Flow.
На Outputs можно ссылаться при заполнении форм Flow или ClusterFlow в пользовательском интерфейсе Rancher.

# Кластерные потоки

Соответствия, фильтры и Outputs настраиваютсядля  ClusterFlows так же, как они настраиваются для Flows. Ключевое отличие состоит в том, что область действия ClusterFlow ограничена на уровне кластера и может настраивать сбор журналов во всех пространствах имен.
ClusterFlows можно настроить, заполнив формы в пользовательском интерфейсе Rancher.
После ClusterFlow выбирает журналы из всех пространств имен в кластере, журналы из кластера будут собираться и записываться в выбранный файл ClusterOutput.

## Пример YAML

В следующем примере Flow сообщения журнала преобразуются из пространства имен по умолчанию и отправляются на S3 Output:

```apiVersion: logging.banzaicloud.io/v1beta1
kind: Flow
metadata:
  name: flow-sample
  namespace: default
spec:
  filters:
    - parser:
        remove_key_name_field: true
        parse:
          type: nginx
    - tag_normaliser:
        format: ${namespace_name}.${pod_name}.${container_name}
  localOutputRefs:
    - s3-output
  match:
    - select:
        labels:
          app: nginx
```
