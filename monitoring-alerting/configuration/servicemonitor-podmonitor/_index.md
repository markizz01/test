ServiceMonitors и PodMonitors — это псевдо-CRD, которые отображают конфигурацию очистки пользовательского ресурса Prometheus.

Эти объекты конфигурации декларативно указывают конечные точки, из которых Prometheus будет собирать метрики.

ServiceMonitors используются чаще, чем PodMonitors, и мы рекомендуем их для большинства случаев использования.

В этом разделе предполагается, что вы знакомы с тем, как компоненты мониторинга работают вместе. Дополнительные сведения об Alertmanager см . [в этом разделе.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/how-monitoring-works)

# СервисМониторы
Этот псевдо-CRD сопоставляется с разделом конфигурации пользовательского ресурса Prometheus. Он декларативно указывает, как следует отслеживать группы сервисов Kubernetes.

Когда создается ServiceMonitor, оператор Prometheus обновляет конфигурацию очистки Prometheus, чтобы включить конфигурацию ServiceMonitor. Затем Prometheus начинает собирать метрики с конечной точки, определенной в ServiceMonitor.

Любые службы в вашем кластере, которые соответствуют меткам, расположенным в поле selector ServiceMonitor, будут отслеживаться на основе указанного endpoints в ServiceMonitor. Для получения дополнительной информации о том, какие поля можно указать, см. [спецификацию](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md ), предоставленную Prometheus Operator.
Для получения дополнительной информации о том, как работают ServiceMonitors, обратитесь к документации [Prometheus Operator.](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/user-guides/running-exporters.md)
Подмониторы
Этот псевдо-CRD сопоставляется с разделом конфигурации пользовательского ресурса Prometheus. Он декларативно указывает, как следует отслеживать группу модулей.

Когда создается PodMonitor, оператор Prometheus обновляет конфигурацию очистки Prometheus, чтобы включить конфигурацию PodMonitor. Затем Prometheus начинает собирать метрики с конечной точки, указанной в PodMonitor.

Любые поды в вашем кластере, которые соответствуют меткам, расположенным в поле selector  PodMonitor, будут отслеживаться на основе указанного podMetricsEndpoints в PodMonitor. Для получения дополнительной информации о том, какие поля можно указать, см. [спецификацию ](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md) , предоставленную Prometheus Operator.
