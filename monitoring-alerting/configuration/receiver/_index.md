Alertmanager Config Secret содержит пример конфигурации Alertmanager, который отправляет уведомления на основе предупреждений, полученных от Prometheus.

В этом разделе предполагается, что вы знакомы с тем, как компоненты мониторинга работают вместе. Дополнительные сведения об Alertmanager см . в этом разделе. docs/content/rancher/v2.6/en/monitoring-alerting/how-monitoring-works/
-	Создание приемников в пользовательском интерфейсе Rancher
-	Конфигурация приемника
-	Slack
-	Email
-	PagerDuty
-	Opsgenie
-	Webhook
-	Custom
-	Teams
-	SMS
-	Настройка нескольких приемников
-	Пример конфигурации Alertmanager
-	Настройка Route Config для CIS Scan Alerts
-	Доверенный CA для уведомителей

# Создание приемников в пользовательском интерфейсе Rancher

Предпосылки:
-	Необходимо установить приложение мониторинга.
-	Если вы настроили мониторинг с помощью существующего Alertmanager Secret, он должен иметь формат, поддерживаемый пользовательским интерфейсом Rancher. В противном случае вы сможете вносить изменения только путем прямого изменения Alertmanager Secret. Примечание. 

Чтобы создать приемники уведомлений в пользовательском интерфейсе Rancher

**Rancher v2.6.5+**
1.	Перейдите в кластер, в котором вы хотите создать приемники. Щелкните **Monitoring -> Alerting -> AlertManagerConfigs**
2.	Щелкните **Создать(Create) .**
3.	Щелкните **добавить получателя.( Add Receiver)**
4.	Введите **Имя (Name)** получателя.
5.	Настройте одного или нескольких провайдеров для получателя. Чтобы получить помощь при заполнении форм, обратитесь к параметрам конфигурации ниже.
6.	Щелкните **Создать(Create).**

**Rancher до v2.6.5**
1.	Перейдите в кластер, в котором вы хотите создать приемники. Нажмите **«Monitoring»** и нажмите **«Приемник» (Receiver) .**
2.	Введите имя получателя.
3.	Настройте одного или нескольких провайдеров для получателя. Чтобы получить помощь при заполнении форм, обратитесь к параметрам конфигурации ниже.
4.	Щелкните **Создать(Create).**


**Результат:** Оповещения можно настроить для отправки уведомлений получателям.

# Конфигурация приемника
Интеграция уведомлений настроена с помощью receiver, что объясняется в документации [Prometheus.](https://prometheus.io/docs/alerting/latest/configuration/#receiver)

# Встроенные и невстроенные приемники
По умолчанию AlertManager обеспечивает встроенную интеграцию с некоторыми приемниками, перечисленными в [этом разделе.](https://prometheus.io/docs/alerting/latest/configuration/#receiver). Все изначально поддерживаемые приемники настраиваются через пользовательский интерфейс Rancher.

Для механизмов уведомления, изначально не поддерживаемых AlertManager, интеграция достигается с помощью приемника [веб-перехватчиков.](https://prometheus.io/docs/alerting/latest/configuration/#webhook_config). Список сторонних драйверов, обеспечивающих такую ​​интеграцию, можно найти здесь.   (https://prometheus.io/docs/operating/integrations/#alertmanager-webhook-receiver). Доступ к этим драйверам и связанным с ними интеграциям предоставляется через приложение Alerting Drivers. После включения настройку неродных приемников также можно выполнить через пользовательский интерфейс Rancher.

В настоящее время приложение Rancher Alerting Drivers предоставляет доступ к следующим интеграциям:
-	Microsoft Teams на основе драйвера [prom2teams](https://github.com/idealista/prom2teams)
-	SMS на основе драйвера [Sachet](https://github.com/messagebird/sachet)

В пользовательском интерфейсе Rancher можно настроить следующие типы приемников:

-	[Slack](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#slack)
-	[Email](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#email)
-	[PagerDuty](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#pagerduty)
-	[Opsgenie](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#opsgenie)
-	[Webhook](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#webhook)
-	[Custom](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#custom)
-	[Teams](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#teams)
-	[SMS](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#sms)

Опцию пользовательского приемника можно использовать для настройки любого приемника в YAML, который нельзя настроить, заполнив другие формы в пользовательском интерфейсе Rancher.

## Slack

|Поле	|Тип|	Описание|
|-|-|-|
|URL-адрес	|String|	Введите URL-адрес веб-перехватчика Slack. Инструкции по созданию веб-перехватчика Slack см. [в документации Slack.](https://slack.com/help/articles/115005265063-%D0%92%D1%85%D0%BE%D0%B4%D1%8F%D1%89%D0%B8%D0%B5-%D0%B2%D0%B5%D0%B1-%D0%BF%D0%B5%D1%80%D0%B5%D1%85%D0%B2%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%B8-%D0%B4%D0%BB%D1%8F-Slack)| 
|Канал по умолчанию|	String|	Введите имя канала, на который вы хотите отправлять оповещения, в следующем формате: #<channelname>.|
|URL-адрес прокси|	String	|Прокси для уведомлений вебхуков.|
|Включить отправку разрешенных предупреждений	|Bool	|Следует ли отправлять последующее уведомление, если предупреждение было разрешено (например, [Решено] Высокая загрузка ЦП).|

## Email
  
|Поле	|Тип	|Описание|
|-|-|-|
|Адрес получателя по умолчанию|	String	|Адрес электронной почты, на который будут приходить уведомления.|
|Включить отправку разрешенных предупреждений	|Bool	|Следует ли отправлять последующее уведомление, если предупреждение было разрешено (например, [Решено] Высокая загрузка ЦП).|

## Параметры SMTP
  
|Поле	|Тип|	Описание|
|-|-|-|
|Отправитель	|String	|Введите адрес электронной почты, доступный на вашем почтовом SMTP-сервере, с которого вы хотите отправить уведомление.|
|Хозяин	|String|	Введите IP-адрес или имя хоста для вашего SMTP-сервера. Пример: smtp.email.com.|
|Используйте TLS|	Bool	|Используйте TLS для шифрования.|
|Имя пользователя	|String|Введите имя пользователя для аутентификации на SMTP-сервере.|
|Пароль	|String	|Введите пароль для аутентификации на SMTP-сервере.|

## PagerDuty
  
|Поле	|Тип	|Описание|
|-|-|-|
|Тип интеграции|	String	|Events API v2или Prometheus.|
|Ключ интеграции по умолчанию|	String|	Инструкции по получению ключа интеграции см. [в документации PagerDuty.](https://www.pagerduty.com/docs/guides/prometheus-integration-guide/)|
|URL-адрес прокси|	String	|Прокси для уведомлений PagerDuty.|
|Включить отправку разрешенных предупреждений|	Bool|	Следует ли отправлять последующее уведомление, если предупреждение было разрешено (например, [Решено] Высокая загрузка ЦП).|

## Opsgenie
  
|Поле|	Описание|
|-|-|
|API-ключ	|Инструкции по получению ключа API см. в документации [Opsgenie.](https://support.atlassian.com/opsgenie/docs/api-key-management/)|
|URL-адрес прокси|	Прокси для уведомлений Opsgenie.|
|Включить отправку разрешенных предупреждений	|Следует ли отправлять последующее уведомление, если предупреждение было разрешено (например, [Решено] Высокая загрузка ЦП).|

## Отвечает Opsgenie
  
|Поле	|Тип	|Описание|
|-|-|-|
|Тип	|String	|Расписание, команда, пользователь или эскалация. Дополнительные сведения об ответчиках предупреждений см. в документации [Opsgenie.](https://support.atlassian.com/opsgenie/docs/who-are-alert-responders/)|
|Отправить	|String|	Идентификатор, имя или имя пользователя получателя Opsgenie.|

## Webhook

|Поле	|Описание|
|-|-|
|URL-адрес	|URL-адрес веб-перехватчика для выбранного вами приложения.|
|URL-адрес прокси|	Прокси для уведомления вебхука.|

Включить отправку разрешенных предупреждений	Следует ли отправлять последующее уведомление, если предупреждение было разрешено (например, [Решено] Высокая загрузка ЦП).

## Custom
 Предоставленный здесь YAML будет напрямую добавлен к вашему приемнику в Alertmanager Config Secret.

# Команды
## Включение приемника Teams для кластеров, управляемых Rancher

  Приемник Teams не является собственным приемником и должен быть включен, прежде чем его можно будет использовать. Вы можете включить приемник Teams для кластера, управляемого Rancher, перейдя на страницу приложений и установив приложение rancher-alerting-drivers с выбранным параметром Teams.
1.	В пользовательском интерфейсе Rancher перейдите к кластеру, в котором вы хотите установить драйверы-предупреждения-ранчера, и нажмите **«Приложения и рынок» (Apps & Marketplace).**
2.	Щелкните приложение **Alerting Drivers.**
3.	Перейдите на вкладку «Параметры развертывания **Helm (Helm Deploy Options) ».**
4.	Выберите параметр **« Teams »** и нажмите **« Установить (Install) » .**
5.	Обратите внимание на используемое пространство имен, так как оно потребуется на более позднем этапе.

## Настройка приемника Teams
Приемник Teams можно настроить, обновив его ConfigMap. Например, ниже приведена минимальная конфигурация приемника Teams.
  ```
[Microsoft Teams]
teams-instance-1: https://your-teams-webhook-url
  ```
По завершении настройки добавьте приемник, следуя инструкциям в этом разделе: [Создание приемников в пользовательском интерфейсе Rancher](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#creating-receivers-in-the-rancher-ui)
  
Используйте приведенный ниже пример в качестве URL-адреса, где:
-	ns-1 заменяется пространством имен rancher-alerting-drivers, в котором установлено приложение 
  ```
url: http://rancher-alerting-drivers-prom2teams.ns-1.svc:8089/v2/teams-instance-1
sms
  ```
  
# Включение приемника SMS для кластеров, управляемых Rancher
Приемник SMS не является родным получателем и должен быть включен, прежде чем его можно будет использовать. Вы можете включить приемник SMS для кластера, управляемого Rancher, перейдя на страницу приложений и установив приложение rancher-alerting-drivers с выбранным параметром SMS.
1.	В левом верхнем углу нажмите **☰ > Управление кластером (Cluster Management ).**
2.	На странице Кластеры перейдите к кластеру, который вы хотите установить, rancher-alerting-driversи нажмите **Explore (Исследовать) .**
3.	На левой панели навигации нажмите
4.	Щелкните приложение **Alerting Drivers .**
5.	Перейдите на вкладку «Параметры развертывания **Helm (Helm Deploy Options)».**
6.	Выберите опцию SMS и нажмите **« Установить (Install)» .**
7.	Обратите внимание на используемое пространство имен, так как оно потребуется на более позднем этапе.
  
# Настройте приемник SMS
Приемник SMS можно настроить, обновив его ConfigMap. Например, ниже приведена минимальная конфигурация приемника SMS.
  ```
providers:
  telegram:
    token: 'your-token-from-telegram'

receivers:
- name: 'telegram-receiver-1'
  provider: 'telegram'
  to:
    - '123456789'
  ```
По завершении настройки добавьте приемник, следуя инструкциям в этом разделе: [Создание приемников в пользовательском интерфейсе Rancher](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/_index.md#creating-receivers-in-the-rancher-ui).

  Используйте приведенный ниже пример в качестве имени и URL-адреса, где:
-	имя, назначенное приемнику, например, telegram-receiver-1, должно совпадать с именем в поле receivers.name в ConfigMap, например, telegram-receiver-1
-	ns-1 в URL-адресе заменяется пространством имен, в котором установлено приложение rancher-alerting-drivers 
  ```
name: telegram-receiver-1
url http://rancher-alerting-drivers-sachet.ns-1.svc:9876/alert
  ```

  ## Настройка нескольких приемников
Редактируя формы в пользовательском интерфейсе Rancher, вы можете настроить ресурс Receiver со всей информацией, необходимой Alertmanager для отправки предупреждений в вашу систему уведомлений.

  Также можно отправлять оповещения в несколько систем уведомлений. Один из способов — настроить приемник с помощью пользовательского YAML, и в этом случае вы можете добавить конфигурацию для нескольких систем уведомлений, если вы уверены, что обе системы должны получать одни и те же сообщения.

  Вы также можете настроить несколько получателей, используя параметр маршрута continue, чтобы оповещения, отправленные получателю, продолжали оцениваться на следующем уровне дерева маршрутизации, который может содержать другого получателя.

# Пример конфигурации Alertmanager
## Slack 
Чтобы настроить уведомления через Slack, следующий YAML Alertmanager Config можно поместить в ключ alertmanager.yaml Alertmanager Config Secret, где его api_url следует обновить, чтобы использовать URL-адрес веб-перехватчика из Slack:
```
  route:
  group_by: ['job']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 3h
  receiver: 'slack-notifications'
receivers:
- name: 'slack-notifications'
  slack_configs:
  - send_resolved: true
    text: '{{ template "slack.rancher.text" . }}'
    api_url: <user-provided slack webhook url here>
templates:
- /etc/alertmanager/config/*.tmpl
```
  
## PagerDuty
Чтобы настроить уведомления через PagerDuty, используйте приведенный ниже пример из документации [PagerDuty](https://www.pagerduty.com/docs/guides/prometheus-integration-guide/)  в качестве руководства. В этом примере настраивается маршрут, который собирает предупреждения для службы базы данных и отправляет их получателю, связанному со службой, которая будет напрямую уведомлять администраторов баз данных в PagerDuty, в то время как все остальные предупреждения будут направляться получателю по умолчанию с другим ключом интеграции PagerDuty.
Следующий YAML конфигурации Alertmanager можно поместить в ключ  alertmanager.yaml Alertmanager Config Secret. Необходимо  обновить service_key, чтобы использовать ваш ключ интеграции PagerDuty, и его можно найти в разделе «Интеграция с глобальной маршрутизацией событий» документации PagerDuty. Полный список опций конфигурации смотрите в документации [Prometheus](https://prometheus.io/docs/alerting/latest/configuration/#pagerduty_config). 
```
route:
 group_by: [cluster]
 receiver: 'pagerduty-notifications'
 group_interval: 5m
 routes:
  - match:
      service: database
    receiver: 'database-notifcations'

receivers:
- name: 'pagerduty-notifications'
  pagerduty_configs:
  - service_key: 'primary-integration-key'

- name: 'database-notifcations'
  pagerduty_configs:
  - service_key: 'database-integration-key'

  ## Пример конфигурации маршрута для предупреждений о сканировании CIS
При настройке маршрутов для оповещений rancher-cis-benchmark можно указать соответствие с помощью пары ключ-значение job: rancher-cis-scan.
Например, следующий пример конфигурации маршрута можно использовать с приемником Slack с именем test-cis:
```  
spec:
  receiver: test-cis
  group_by:
#    - string
  group_wait: 30s
  group_interval: 30s
  repeat_interval: 30s
  match:
    job: rancher-cis-scan
#    key: string
  match_re:
    {}
#    key: string
```  
Дополнительные сведения о включении оповещений для rancher-cis-benchmark, см . [в этом разделе.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/receiver/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cis-scans/)

# Доверенный ЦС для уведомителей
Если вам нужно добавить доверенный центр сертификации в свой уведомитель, выполните действия, описанные в [этом разделе.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/configuration/helm-chart-options#trusted-ca-for-notifiers)
