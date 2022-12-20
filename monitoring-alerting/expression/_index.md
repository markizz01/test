# Справочник по выражениям PromQL

Выражения PromQL в этом документе можно использовать для настройки предупреждений.

Дополнительные сведения о запросах к базе данных временных рядов Prometheus см. в официальной [документации Prometheus.](https://prometheus.io/docs/prometheus/latest/querying/basics/)

-	Метрики кластера
    -	Загрузка ЦП кластера
    -	Средняя нагрузка кластера
    -	Использование памяти кластера
    -	Использование кластерного диска
    -	Дисковый ввод-вывод кластера
    -	Сетевые пакеты кластера
    -	Кластерный сетевой ввод-вывод
-	Метрики узла
    -	Загрузка ЦП узла
    -	Средняя нагрузка узла
    -	Использование памяти узла
    -	Использование диска узла
    -	Дисковый ввод-вывод узла
    -	Сетевые пакеты узла
    -	Сетевой ввод-вывод узла
-	И т. д. Метрики
    -	Ecd имеет лидера
    -	Количество смен лидера
    -	Количество неудачных предложений
    -	Клиентский трафик GRPC
    -	Одноранговый трафик
    -	Размер БД
    -	Активные потоки
    -	Предложения плота
    -	Скорость RPC
    -	Дисковые операции
    -	Продолжительность синхронизации диска
-	Метрики компонентов Kubernetes
    -	Задержка запроса сервера API
    -	Частота запросов к серверу API
    -	Планирование неудачных модулей
    -	Глубина очереди диспетчера контроллеров
    -	Задержка планировщика E2E
    -	Попытки вытеснения планировщика
    -	Соединения контроллера входящего трафика
    -	Время обработки запроса контроллера входящего трафика
-	Метрики ведения журнала Rancher
    -	Частота буферной очереди Fluentd
    -	Свободная скорость ввода
    -	Коэффициент ошибок вывода Fluentd
    -	Скорость вывода Fluentd
-	Показатели рабочей нагрузки
    -	Загрузка ЦП рабочей нагрузки
    -	Использование памяти рабочей нагрузки
    -	Сетевые пакеты рабочей нагрузки
    -	Сетевой ввод-вывод рабочей нагрузки
    -	Дисковый ввод-вывод рабочей нагрузки
-	Метрики пода
    -	Загрузка ЦП пода
    -	Использование памяти модуля
    -	Сетевые пакеты Pod
    -	Сетевой ввод-вывод модуля
    -	Дисковый ввод-вывод модуля
-	Метрики контейнера
    -	Использование ЦП контейнера
    -	Использование памяти контейнера
    -	Дисковый ввод-вывод контейнера

# Метрики кластера
## Загрузка CPU кластера

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|1 - (avg(irate(node\_cpu\_seconds\_total{mode="idle"}[5m])) by (instance))|
|Резюме|1 - (avg(irate(node\_cpu\_seconds\_total{mode="idle"}[5m])))|

## Средняя нагрузка кластера

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|
|нагрузка1|sum(node\_load1) by (instance) / count(node\_cpu\_seconds\_total{mode="system"}) by (instance)|
|нагрузка5|sum(node\_load5) by (instance) / count(node\_cpu\_seconds\_total{mode="system"}) by (instance)|
|нагрузка15|sum(node\_load15) by (instance) / count(node\_cpu\_seconds\_total{mode="system"}) by (instance)||
|Резюме|
|нагрузка1|sum(node\_load1) by (instance) / count(node\_cpu\_seconds\_total{mode="system"})|
|нагрузка5|sum(node\_load5) by (instance) / count(node\_cpu\_seconds\_total{mode="system"})|
|нагрузка15|sum(node\_load15) by (instance) / count(node\_cpu\_seconds\_total{mode="system"})||


## Использование памяти кластера

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|1 - sum(node\_memory\_MemAvailable\_bytes) by (instance) / sum(node\_memory\_MemTotal\_bytes) by (instance)|
|Резюме|1 - sum(node\_memory\_MemAvailable\_bytes) / sum(node\_memory\_MemTotal\_bytes)|
**Использование Cluster Disk** 

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь|(sum(node\_filesystem\_size\_bytes{device!="rootfs"}) by (instance) - sum(node\_filesystem\_free\_bytes{device!="rootfs"}) by (instance)) / sum(node\_filesystem\_size\_bytes{device!="rootfs"}) by (instance)|
|Резюме|(sum(node\_filesystem\_size\_bytes{device!="rootfs"}) - sum(node\_filesystem\_free\_bytes{device!="rootfs"})) / sum(node\_filesystem\_size\_bytes{device!="rootfs"})|

## Дисковый ввод-вывод кластера (Cluster Disk I/O)

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||

|читать|sum(rate(node\_disk\_read\_bytes\_total[5m])) by (instance)|
| :- | :- |
|написано|sum(rate(node\_disk\_written\_bytes\_total[5m])) by (instance)|

|| |
| :- | :- |
|Резюме||

|читать|sum(rate(node\_disk\_read\_bytes\_total[5m]))|
| :- | :- |
|написано|sum(rate(node\_disk\_written\_bytes\_total[5m]))|

|| |
| :- | :- |

## Сетевые пакеты кластера Cluster Network Packets

|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||

|получить-выпало|sum(rate(node\_network\_receive\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)|
| :- | :- |
|прием-ошибки|sum(rate(node\_network\_receive\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|получить-пакеты|sum(rate(node\_network\_receive\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|передача сбрасывается|sum(rate(node\_network\_transmit\_drop\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|ошибки передачи|sum(rate(node\_network\_transmit\_errs\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m])) by (instance)*|
|передавать-пакеты|sum(rate(node\_network\_transmit\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)|

|| |
| :- | :- |
|Резюме||

|получить-выпало|sum(rate(node\_network\_receive\_drop\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))|
| :- | :- |
|прием-ошибки|sum(rate(node\_network\_receive\_errs\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|получить-пакеты|sum(rate(node\_network\_receive\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|передача сбрасывается|sum(rate(node\_network\_transmit\_drop\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|ошибки передачи|sum(rate(node\_network\_transmit\_errs\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.*"}[5m]))*|
|передавать-пакеты|sum(rate(node\_network\_transmit\_packets\_total{device!~"lo | veth. | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))|

|| |
| :- | :- |

## Cluster Network I/O



|**Каталог**|**Выражение**|
| :-: | :-: |
|Деталь||

|Получать|sum(rate(node\_network\_receive\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)|
| :- | :- |
|передавать|sum(rate(node\_network\_transmit\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m])) by (instance)|

|| |
| :- | :- |
|Резюме||

|Получать|sum(rate(node\_network\_receive\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))|
| :- | :- |
|передавать|sum(rate(node\_network\_transmit\_bytes\_total{device!"lo | veth.\* | docker.\* | flannel.\* | cali.\* | cbr.\*"}[5m]))|

|| |
| :- | :- |
