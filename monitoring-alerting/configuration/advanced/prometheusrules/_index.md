PrometheusRule определяет группу правил предупреждений и/или записи Prometheus.

В этом разделе предполагается, что вы знакомы с тем, как компоненты мониторинга работают вместе. Для получения дополнительной информации см. [этот раздел.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/prometheusrules/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/monitoring-alerting/how-monitoring-works)

# Создание правил Prometheus в пользовательском интерфейсе Rancher

Необходимое условие: необходимо установить приложение для мониторинга.

Чтобы создать группы правил в пользовательском интерфейсе Rancher,
1.	Перейдите к кластеру, в котором вы хотите создать группы правил. Нажмите **Monitoring > Advanced(дополнительно)** и нажмите **«Prometheus Rules» .**
2.	Щелкните **(Создать) Create.**
3.	Введите **имя группы.**
4.	Настройте правила. В пользовательском интерфейсе Rancher мы ожидаем, что группа правил будет содержать либо правила предупреждений, либо правила записи, но не то и другое одновременно. Чтобы получить помощь при заполнении форм, обратитесь к параметрам конфигурации ниже.
5.	Щелкните **(Создать) Create.**

**Результат:** Оповещения можно настроить для отправки уведомлений получателям.

## О пользовательском ресурсе PrometheusRule

Когда вы определяете правило (которое объявлено в RuleGroup в ресурсе PrometheusRule), [спецификация самого правила](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md) содержит метки, которые используются Alertmanager для определения того, какой маршрут должен получать это предупреждение. Например, оповещение с меткой team: front-end будет отправлено на все маршруты, соответствующие этой метке.

Файлы правил Prometheus хранятся в пользовательских ресурсах PrometheusRule. PrometheusRule позволяет определить одну или несколько групп правил. Каждая RuleGroup состоит из набора объектов Rule, каждый из которых может представлять либо предупреждение, либо правило записи со следующими полями:
-	Имя нового оповещения или записи
-	Выражение PromQL для нового оповещения или записи.
-	Метки, которые должны быть прикреплены к предупреждению или записи, идентифицирующие его (например, имя кластера или его тяжесть).
-	Аннотации, кодирующие любые дополнительные важные сведения, которые необходимо отображать в уведомлении для оповещения (например, аннотация, описание, сообщение, URL-адрес модуля Runbook и т. д.). Это поле не требуется для записи правил.

Дополнительные сведения о том, какие поля можно указать, см. [в спецификации оператора Prometheus.](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md)

Используйте поле селектора меток ruleSelector в объекте Prometheus, чтобы определить файлы правил, которые вы хотите смонтировать в Prometheus.

Примеры см. в документации Prometheus по [правилам записи](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/)   и правилам [оповещения](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/).

# Конфигурация
## Группа правил

|Поле|	Описание|
|-|-|
|Название группы|	Название группы. Должен быть уникальным в пределах файла правил.|
|Переопределить групповой интервал|	Продолжительность в секундах того, как часто оцениваются правила в группе.|

## Правила предупреждений
[Правила оповещения](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)  позволяют вам определять условия оповещения на основе выражений PromQL (Prometheus Query Language) и отправлять уведомления об срабатывании оповещений во внешнюю службу.

|Поле|	Описание|
|-|-|
|Имя оповещения	|Название оповещения. Должно быть допустимым значением метки.|
|Wait To Fire For	|Продолжительность в секундах. Оповещения считаются активированными, если они возвращаются в течение этого времени. Оповещения, которые еще не срабатывали достаточно долго, считаются ожидающими.|
|PromQL Expression	|Выражение PromQL для оценки. Prometheus будет оценивать текущее значение этого выражения PromQL в каждом цикле оценки, и все результирующие временные ряды станут ожидающими/активируемыми предупреждениями. Для получения дополнительной информации обратитесь к [документации Prometheus](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)  или нашим примерам [выражений PromQL.](https://github.com/rancher/docs/tree/master/content/rancher/v2.6/en/monitoring-alerting/expression)|
|Labels	|Ярлыки, которые нужно добавить или перезаписать для каждого оповещения.|
|Severity	|Если этот параметр включен, к предупреждению или записи прикрепляются метки, которые идентифицируют их по уровню серьезности.|
|Severity Label Value|	Критический, предупреждение или отсутствие|
|Annotations|	Аннотации — это набор информационных меток, которые можно использовать для хранения дополнительной информации, например, описаний предупреждений или ссылок на модули Runbook. Runbook — это набор документации о том, как обрабатывать оповещения . Значения аннотаций могут быть [шаблонными.](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/#templating)|

## Правила записи
[Правила записи](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/#recording-rules)  позволяют предварительно вычислять часто используемые или ресурсоемкие выражения PromQL (Prometheus Query Language) и сохранять их результат в виде нового набора временных рядов.

|Поле	|Описание|
|-|-|
|Название временного ряда	|Имя временного ряда для вывода. Должно быть допустимым именем метрики.|
|PromQL Expression	|Выражение PromQL для оценки. Prometheus будет оценивать текущее значение этого выражения PromQL в каждом цикле оценки, и результат будет записываться как новый набор временных рядов с именем метрики, заданным «записью». Для получения дополнительной информации о выражениях обратитесь к [документации Prometheus](https://prometheus.io/docs/prometheus/latest/querying/basics/)  или нашему примеру [выражений PromQL.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/monitoring-alerting/configuration/advanced/expression)|
|Labels	|Метки, которые необходимо добавить или перезаписать перед сохранением результата.|
