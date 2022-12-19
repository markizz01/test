# Конфигурация диспетчера предупреждений
-	Настройка лимитов ресурсов и запросов
-	Доверенный CA для уведомителей
-	Дополнительные конфигурации очистки
-	Настройка приложений, упакованных в Monitoring V2
-	Увеличьте количество реплик Alertmanager
-	Настройка пространства имен для постоянной панели управления Grafana


# Настройка лимитов ресурсов и запросов
Запросы ресурсов и лимиты можно настроить при установке rancher-monitoring.
Значения по умолчанию находятся в файле values.yaml (https://github.com/rancher/charts/blob/main/charts/rancher-monitoring/values.yam) l на rancher-monitoring диаграмме Helm.
Значения по умолчанию в таблице ниже — это минимальные требуемые лимиты ресурсов и запросы.

|Имя ресурса	|Лимит памяти	|Лимит ЦП	|Запрос памяти	|Запрос процессора|
|-|-|-|-|-|
|alertmanager	|500 миль|	1000м	|100 миль	|100м|
|grafana|	200 миль|	200м	|100 миль	|100м
|kube-state-metrics subchart	|200 миль|	100м	|130 миль|	100м|
|prometheus-node-exporter subchart|	50 миль	|200м	|30 миль|	100м|
|prometheusOperator|	500 миль|	200м|	100 миль|	100м|
|prometheus|	2500 миль	|1000м	|1750 миль|	750м|
|-|-|-|-|-|
|Общий	|3950Ми|	2700м	|2210Ми|	1250м|

Рекомендуется хранилище не менее 50Gi.

# Доверенный CA для уведомителей
Если вам нужно добавить доверенный CA в свой уведомитель, выполните следующие действия:
1.	Создайте пространство имен cattle-monitoring-system.
2.	Добавьте доверенного CA secret в cattle-monitoring-system.
3.	Разверните или обновите rancher-monitoring Helm chart. В параметрах диаграммы укажите secret в Alerting > Additional Secrets .

**Результат:** Пользовательский ресурс Alertmanager по умолчанию будет иметь доступ к вашему доверенному CA.

# Дополнительные Scrape Configurations  (конфигурации очистки)

Если требуемую Scrape Configurations нельзя указать через ServiceMonitor или PodMonitor в данный момент, вы можете предоставить при развертывании additionalScrapeConfigSecret или при обновлении файл rancher-monitoring.
Раздел [scrape_config](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#scrape_config)  определяет набор целей и параметров, описывающих, как их очищать. В общем случае одна конфигурация очистки определяет одно задание.

Примером того, где это можно использовать, является Istio. Для получения дополнительной информации см. [этот раздел.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/helm-chart-options/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/istio/configuration-reference/selectors-and-scrape)

# Настройка приложений, упакованных в Monitoring v2

Разворачиваем kube-state-metrics и node-exporter с мониторингом v2. Экспортер узлов развертывается как DaemonSets. В контрольной диаграмме Monitoring v2 в файле values.yaml каждая из них развертывается как sub charts.

Мы также развертываем grafana, которым не управляет prometheus.

Если вы посмотрите на то, как работает helm в kube-state-metrics, то увидите, что вы можете установить гораздо больше значений, которые не отображаются на chart верхнего уровня.

Но в chart верхнего уровня вы можете добавить значения, которые переопределяют значения, существующие в sub chart (подразделе).

# Увеличьте количество реплик Alertmanager

В рамках вариантов развертывания чарта вы можете увеличить количество реплик Alertmanager, развернутых в вашем кластере. Всеми репликами можно управлять с помощью одного и того же базового Alertmanager Config Secret. Дополнительные сведения о Alertmanager Config Secret см. [в этом разделе.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/alertmanager#multiple-alertmanager-replicas)

# Настройка пространства имен для постоянной панели управления Grafana

Чтобы указать, что вы хотите, чтобы Grafana отслеживала ConfigMaps во всех пространствах имен, установите это значение в rancher-monitoring Helm chart:
grafana.sidecar.dashboards.searchNamespace=ALL

Обратите внимание, что роли RBAC, представленные Monitoring chart для добавления панелей мониторинга Grafana, по-прежнему ограничены предоставлением пользователям разрешений на добавление панелей мониторинга в пространство имен, определенное в grafana.dashboards.namespace, которое по умолчанию равно cattle-dashboards.
