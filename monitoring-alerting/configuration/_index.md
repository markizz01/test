На этой странице представлены некоторые наиболее важные параметры настройки Monitoring V2 в пользовательском интерфейсе Rancher.

Для получения информации о настройке пользовательских целей очистки и правил для Prometheus обратитесь к исходной документации для [оператора Prometheus.](https://github.com/prometheus-operator/prometheus-operator).  Некоторые из наиболее важных пользовательских ресурсов описаны в проектной документации [Prometheus Operator.](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/design.md).  Документация Prometheus Operator также может помочь вам настроить RBAC, Thanos или пользовательскую конфигурацию.

# Установка лимитов ресурсов и запросов
Запросы ресурсов и ограничения для приложения мониторинга можно настроить при установке rancher-monitoring. Дополнительные сведения об ограничениях по умолчанию см . [на этой странице.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/configuration/helm-chart-options#configuring-resource-limits-and-requests) 

***Примечание.** В неактивном кластере Monitoring V2 имеет значительно более высокую загрузку ЦП (до 70%) по сравнению с Monitoring V1. Для повышения производительности и получения результатов, подобных Мониторингу V1, отключите адаптер Prometheus.*

# Конфигурация Prometheus
Обычно нет необходимости напрямую редактировать пользовательский ресурс Prometheus.

Вместо этого, чтобы настроить Prometheus для очистки пользовательских метрик, вам нужно будет только создать новый ServiceMonitor или PodMonitor, чтобы настроить Prometheus для очистки дополнительных метрик.

# Конфигурация ServiceMonitor и PodMonitor
Подробнее см . [на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/servicemonitor-podmonitor)

# Расширенная конфигурация Prometheus
Для получения дополнительной информации о непосредственном редактировании пользовательского ресурса Prometheus, который может быть полезен в сложных случаях использования, см. [эту страницу.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/prometheus) 

# Конфигурация Alertmanager - диспетчера оповещений
Пользовательский ресурс Alertmanager обычно не нужно редактировать напрямую. В большинстве распространенных случаев вы можете управлять оповещениями, обновляя Routes и Receivers.

Маршруты и получатели являются частью конфигурации пользовательского ресурса Аlertmanager. В пользовательском интерфейсе Rancher маршруты и приемники — это не настоящие настраиваемые ресурсы, а псевдонастраиваемые ресурсы, которые оператор Prometheus использует для синхронизации вашей конфигурации с настраиваемым ресурсом Alertmanager. При обновлении маршрутов и получателей приложение мониторинга автоматически обновит Alertmanager, чтобы отразить эти изменения.

Для некоторых расширенных вариантов использования вы можете настроить alertmanager напрямую. Для получения дополнительной информации см . [эту страницу.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/alertmanager) 

# приемники
Ресиверы используются для настройки уведомлений. Подробнее о настройке приемников см . [на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver)

# Маршруты
Маршруты фильтруют уведомления до того, как они достигнут получателей. Каждый маршрут должен ссылаться на приемник, который уже настроен. Подробнее о настройке маршрутов см . [на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/route)

# дополнительно
Для получения дополнительной информации о непосредственном редактировании пользовательского ресурса Alertmanager, который может быть полезен в сложных случаях использования, см. [эту страницу.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/alertmanager)
