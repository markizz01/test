|||
|:-|:-|
|Taints and Tolerations||

«Заражение» узла Kubernetes приводит к тому, что модули отказываются работать на этом узле.

Если у модулей будет toleration, то при «заражении» этого узла, они будут работать на других узлах в кластере.

Заражения и допуски https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/ могут работать в сочетании с полем https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector nodeSelector  внутри PodSpec, что обеспечивает эффект противоположный заражению.

Использование nodeSelector придает модулям сходство с определенными узлами.

Оба предоставляют выбор для того, на каком узле (ах) будет работать модуль.
-	Реализация по умолчанию в стеке регистрации Rancher
-	Добавление настроек NodeSelector и допусков для пользовательских Taints


# Реализация по умолчанию в стеке регистрации Rancher

По умолчанию Rancher заражает все узлы Linux cattle.io/os=linux и не заражает узлы Windows. Модули стека ведения журналов имеют tolerations к заражению, что позволяет им работать на узлах Linux. Более того, большинство модулей стека ведения журналов работают только в Linux и имеют nodeSelector добавленное, для обеспечения их работы на узлах Linux.

Этот пример файла Pod YAML показывает, что nodeSelector используется с допуском:
```
apiVersion: v1
kind: Pod
# metadata...
spec:
  # containers...
  tolerations:
    - key: cattle.io/os
      operator: "Equal"
      value: "linux"
      effect: NoSchedule
  nodeSelector:
    kubernetes.io/os: linux
```
В приведенном выше примере мы гарантируем, что наш модуль работает только на узлах Linux, и добавляем toleration для всех наших узлов Linux.

Вы можете сделать то же самое с существующими заражениями Rancher или со своими собственными.

# Добавление настроек NodeSelector и допусков для пользовательских Taints

Если вы хотите добавить свои собственные настройки nodeSelector или добавить дополнительные пометки tolerations, вы можете добавить следующее в значения диаграммы.
```
tolerations:
  # insert tolerations...
nodeSelector:
  # insert nodeSelector...
```
Эти значения добавят обе настройки в контейнеры fluentd, fluentbit и logging-operator. По сути, это глобальные настройки для всех модулей в стеке журналирования.
Однако, если вы хотите добавить допуски только для контейнера fluentbit, вы можете добавить следующее к значениям диаграммы. 

```
fluentbit_tolerations:
  # insert tolerations list for fluentbit containers only...
```
