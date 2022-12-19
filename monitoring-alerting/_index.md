Используя rancher-monitoring приложение, вы можете быстро развернуть в своем кластере ведущие решения для мониторинга и оповещения с открытым исходным кодом.

# Функции

Prometheus позволяет вам просматривать метрики ваших объектов Rancher и Kubernetes. Используя временные метки, Prometheus позволяет вам запрашивать и просматривать эти показатели в виде удобных для чтения графиков и визуальных элементов либо через пользовательский интерфейс Rancher, либо через Grafana, платформу для просмотра аналитики, развернутую вместе с Prometheus.

Просматривая данные, которые Prometheus извлекает из плоскости управления вашего кластера, узлов и развертываний, вы можете быть в курсе всего, что происходит в вашем кластере. Затем вы можете использовать эту аналитику, чтобы лучше управлять своей организацией: останавливать аварийные ситуации в системе до того, как они начнутся, разрабатывать стратегии обслуживания или восстанавливать поврежденные серверы.

Оператор rancher-monitoring, представленный в Rancher v2.5, работает на [Prometheus](https://prometheus.io/) , [Grafana](https://grafana.com/grafana/) , [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/) , [Prometheus Operator](https://github.com/prometheus-operator/prometheus-operator), и  [Prometheus adapter.](https://github.com/DirectXMan12/k8s-prometheus-adapter)

Приложение мониторинга позволяет:
-	Отслеживать состояние и процессы узлов вашего кластера, компонентов Kubernetes и развертываний программного обеспечения.
-	Определять оповещения на основе метрик, собранных с помощью Prometheus
-	Создавать пользовательские Grafana dashboards
-	Настраивать уведомления на основе предупреждений по электронной почте, Slack, PagerDuty и т. д. с помощью Prometheus Alertmanager.
-	Определять предварительно вычисленные, часто используемые или ресурсоемкие выражения в виде новых временных рядов на основе метрик, собранных с помощью Prometheus.
-	Предоставляйте собранные метрики из Prometheus API пользовательских метрик Kubernetes (Kubernetes Custom Metrics API ) через Prometheus Adapter  для использования в HPA.

# Как работает мониторинг

Объяснение того, как компоненты мониторинга работают вместе, см . [на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/how-monitoring-works) 

# Компоненты и развертывания по умолчанию
## Встроенные информационные панели
По умолчанию приложение мониторинга развертывает информационные панели Grafana (курируемые [проектом kube-prometheus](https://github.com/prometheus-operator/kube-prometheus) ) в кластере.

Он также развертывает пользовательский интерфейс Alertmanager и пользовательский интерфейс Prometheus. Дополнительные сведения об этих инструментах см. в разделе [Встроенные информационные панели.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/dashboards)

## Экспортеры метрик по умолчанию
По умолчанию Rancher Monitoring развертывает экспортеры (например, [node-exporter](https://github.com/prometheus/node_exporter) и [kube-state-metrics](https://github.com/kubernetes/kube-state-metrics) ).
Эти экспортеры по умолчанию автоматически извлекают метрики CPU и памяти из всех компонентов вашего кластера Kubernetes, включая ваши рабочие нагрузки.

## Оповещения по умолчанию
Приложение мониторинга развертывает некоторые оповещения по умолчанию. Чтобы просмотреть оповещения по умолчанию, перейдите в [пользовательский интерфейс Alertmanager](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/dashboards#alertmanager-ui) и щелкните **Expand all groups (Развернуть все группы).**

# Компоненты, представленные в пользовательском интерфейсе Rancher
Список компонентов мониторинга, представленных в пользовательском интерфейсе Rancher, а также распространенные варианты их редактирования см . [в этом разделе.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/how-monitoring-works#components-exposed-in-the-rancher-ui) 

# Управление доступом на основе ролей
Информацию о настройке доступа к мониторингу см . [на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/rbac) 

# Гайды
-	[Включить мониторинг](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/guides/enable-monitoring)
-	[Удалить мониторинг](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/guides/uninstall)
-	[Мониторинг рабочих нагрузок](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/guides/monitoring-workloads)
-	[Настройка информационных панелей Grafana (Grafana dashboards)]()
-	[Постоянные информационные панели Grafana (Grafana dashboards)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/guides/persist-grafana)
-	[Отладка высокого использования памяти](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/guides/memory-usage)
-	[Миграция с мониторинга V1 на V2](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/guides/migrating)

# Конфигурация
## Настройка ресурсов мониторинга в Rancher
Справочник по конфигурации предполагает знакомство с тем, как компоненты мониторинга работают вместе. Дополнительные сведения см. в разделе [Как работает мониторинг.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/how-monitoring-works)
-	[ServiceMonitor and PodMonitor](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/servicemonitor-podmonitor)
-	[Receiver](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver)
-	[Route](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/route)
-	[PrometheusRule](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/prometheusrules)
-	[Prometheus](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/prometheus)
-	[Alertmanager](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/alertmanager)


## Настройка параметров Helm
Для получения дополнительной информации о  параметрах rancher-monitoring, включая параметры для установки лимитов ресурсов и запросов, см. [эту страницу.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/helm-chart-options)

## Поддержка кластера Windows
При развертывании в кластере RKE1 Windows Monitoring V2 теперь автоматически развертывает DaemonSet [windows-exporter](https://github.com/prometheus-community/windows_exporter) и настраивает ServiceMonitor для сбора метрик с каждого из развернутых модулей. Это заполнит Prometheus  метриками windows_, аналогичными  метрикам node_, экспортируемым [node_exporter](https://github.com/prometheus/node_exporter) для хостов Linux.
Чтобы иметь возможность полностью развернуть Monitoring V2 для Windows, на всех ваших хостах Windows должна быть установлена минимальная версия [win](https://github.com/rancher/wins) версии 0.1.0.
Дополнительные сведения о том, как обновить wins на существующих хостах Windows, см. в разделе, посвященном [поддержке кластера Windows для Monitoring V2.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/windows-clusters)

## Известные вопросы
Существует [известная проблема](https://github.com/rancher/rancher/issues/28787#issuecomment-693611821) , связанная с тем, что кластерам K3s требуется больше памяти по умолчанию. Если вы включаете мониторинг в кластере K3s, мы рекомендуем установить prometheus.prometheusSpec.resources.memory.limit2500 Mi и prometheus.prometheusSpec.resources.memory.request1750 Mi.
Советы по устранению чрезмерного использования памяти см . [на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/guides/memory-usage)
