Обычно нет необходимости напрямую редактировать пользовательский ресурс Prometheus, поскольку приложение мониторинга автоматически обновляет его на основе изменений в ServiceMonitors и PodMonitors.

В этом разделе предполагается, что вы знакомы с тем, как компоненты мониторинга работают вместе. Для получения дополнительной информации см. [этот раздел.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/how-monitoring-works) 

# О пользовательском ресурсе Prometheus
Prometheus CR определяет желаемое развертывание Prometheus. Оператор Prometheus наблюдает за КР Prometheus. При изменении CR оператор Prometheus создает prometheus-rancher-monitoring-prometheusразвертывание Prometheus на основе конфигурации CR.

Prometheus CR определяет такие детали: какие правила и какие Alertmanagers подключены к Prometheus. Rancher создает этот CR для вас.

Monitoring V2 поддерживает только один Prometheus на кластер. Однако вы можете отредактировать Prometheus CR, если хотите ограничить мониторинг определенными пространствами имен.
