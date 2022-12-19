# Встроенные информационные панели
-	Grafana UI
-	Alertmanager UI
-	Prometheus UI


##  Пользовательский интерфейс Grafana
[Grafana](https://grafana.com/grafana/) позволяет вам запрашивать, визуализировать, предупреждать и понимать ваши показатели независимо от того, где они хранятся. Создавайте, исследуйте и делитесь информационными панелями со своей командой и развивайте культуру, основанную на данных.

Чтобы просмотреть панели мониторинга по умолчанию для визуализации данных временных рядов, перейдите в пользовательский интерфейс Grafana.

## Настройка Grafana
Чтобы просмотреть и настроить запросы PromQL для панели управления Grafana, см. [эту страницу.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/guides/customize-grafana)

## Постоянные информационные панели Grafana
Чтобы создать постоянную панель управления Grafana, см. [эту страницу.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/guides/persist-grafana) 

## Доступ к Grafana
Сведения об управлении доступом на основе ролей для Grafana см . в [этом разделе.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/rbac#role-based-access-control-for-grafana)

## Пользовательский интерфейс Alertmanager
При  установке rancher-monitoring развертывается пользовательский интерфейс Prometheus Alertmanager, что позволяет вам просматривать свои предупреждения и текущую конфигурацию Alertmanager.

В этом разделе предполагается, что вы знакомы с тем, как компоненты мониторинга работают вместе. Дополнительные сведения об Alertmanager см . [в этом разделе.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/how-monitoring-works#how-alertmanager-works) 

## Доступ к пользовательскому интерфейсу Alertmanager

Пользовательский интерфейс Alertmanager позволяет просматривать самые последние оповещения.
Предварительное **условие:** приложение rancher-monitoring должно быть установлено.

Чтобы увидеть пользовательский интерфейс Alertmanager,
1.	В левом верхнем углу нажмите **☰ > (Cluster Management) Управление кластером .**
2.	На странице **« Кластеры (Clusters) »** перейдите к кластеру, в котором вы хотите увидеть пользовательский интерфейс Alertmanager, нажмите **« Обзор (Explore) » .**
3.	На левой панели навигации щелкните **Мониторинг (Monitoring) .**
4.	Щелкните **Alertmanager.**

**Результат:** Пользовательский интерфейс Alertmanager открывается в новой вкладке. Для получения помощи по настройке обратитесь к официальной документации [Alertmanager.](https://prometheus.io/docs/alerting/latest/alertmanager/)

Для получения дополнительной информации о настройке Alertmanager в Rancher см. [эту страницу.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/alertmanager)

## Просмотр предупреждений по умолчанию
Чтобы просмотреть оповещения, запускаемые по умолчанию, перейдите в пользовательский интерфейс Alertmanager и щелкните **Expand all groups (Развернуть все группы).**

## Пользовательский интерфейс Prometheus
По умолчанию [служба kube-state-metrics](https://github.com/kubernetes/kube-state-metrics) предоставляет приложению мониторинга обширную информацию об использовании CPU и памяти. Эти метрики охватывают ресурсы Kubernetes в разных пространствах имен. Это означает, что для просмотра метрик ресурсов для службы вам не нужно создавать для нее новый ServiceMonitor. Поскольку данные уже находятся во временных рядах базы данных, вы можете перейти в пользовательский интерфейс Prometheus и выполнить запрос PromQL, чтобы получить информацию. Тот же запрос можно использовать для настройки панели мониторинга Grafana для отображения графика этих показателей с течением времени.

Чтобы увидеть пользовательский интерфейс Prometheus, установите rancher-monitoring. 

Затем:
1.	В левом верхнем углу нажмите **☰ > Управление кластером (Cluster Management) .**
2.	На странице **Clusters** перейдите к кластеру, в котором вы хотите увидеть пользовательский интерфейс Prometheus, и нажмите **Explore .**
3.	На левой панели навигации щелкните **Monitoring (Мониторинг) .**
4.	Щелкните **Prometheus Graph.**


## Просмотр целей Prometheus
Чтобы увидеть, какие службы вы отслеживаете, вам нужно будет увидеть свои цели. Цели устанавливаются ServiceMonitors и PodMonitors в качестве источников для извлечения метрик. Вам не нужно будет напрямую редактировать цели, но пользовательский интерфейс Prometheus может быть полезен для предоставления вам обзора всех источников метрик, которые анализируются.

Чтобы увидеть цели Prometheus, установите rancher-monitoring. Затем:
1.	В левом верхнем углу нажмите **☰ > Cluster Management (Управление кластером) .**
2.	На странице **Clusters** перейдите к кластеру, в котором вы хотите увидеть цели Prometheus, и нажмите **Explore .**
3.	На левой панели навигации щелкните **Monitoring (Мониторинг) .**
4.	Щелкните **Prometheus Targets.**


## Просмотр PrometheusRules
Когда вы определяете правило (которое объявлено в RuleGroup в ресурсе PrometheusRule), спецификация [самого правила](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md) содержит метки, которые используются Alertmanager для определения того, какой маршрут должен получать определенное предупреждение.

Чтобы увидеть PrometheusRules, установите rancher-monitoring. Затем:
1.	В левом верхнем углу нажмите **☰ > Cluster Management.(Управление кластером) .**
2.	На странице **« Кластеры (Clusters)»** перейдите к кластеру, в котором вы хотите просмотреть визуализации, и нажмите **« Explore » .**
3.	На левой панели навигации щелкните **Monitoring.**
4.	Щелкните **Prometheus Rules.**


Вы также можете увидеть правила в пользовательском интерфейсе Prometheus.

Для получения дополнительной информации о настройке PrometheusRules в Rancher см. [эту страницу.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/prometheusrules)
