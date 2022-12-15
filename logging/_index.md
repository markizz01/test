Rancher интегрируется с популярными сервисами ведения журналов. Узнайте о требованиях и преимуществах интеграции со службами ведения журналов и включите ведение журналов в своем кластере

Оператор Banzai Cloud Logging теперь поддерживает решение Rancher для ведения журналов вместо прежнего внутреннего решения.

Обзор изменений в версии 2.5 [см . в этом разделе.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/logging/architecture/.)  Сведения о переходе с Logging V1 [см . на этой странице.](https://github.com/rancher/docs/tree/master/content/rancher)

-	[Включение ведения журнала](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%B0)
-	[Удалить ведение журнала](https://github.com/markizz01/test/blob/main/logging/_index.md#%D1%83%D0%B4%D0%B0%D0%BB%D0%B8%D1%82%D1%8C-%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%B0)
-	[Архитектура](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D0%B0)
-	[Управление доступом на основе ролей](https://github.com/markizz01/test/blob/main/logging/_index.md#%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%BE%D0%BC-%D0%BD%D0%B0-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%B5-%D1%80%D0%BE%D0%BB%D0%B5%D0%B9)
-	[Настройка пользовательских ресурсов ведения журнала](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D1%81%D0%BA%D0%B8%D1%85-%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%BE%D0%B2)
    -	[Потоки и кластерные потоки](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B8-%D0%B8-%D0%BA%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%BD%D1%8B%D0%B5-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B8)
    -	[Выходы и кластерные выходы](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%B2%D1%8B%D1%85%D0%BE%D0%B4%D1%8B-%D0%B8-%D0%BA%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%BD%D1%8B%D0%B5-%D0%B2%D1%8B%D1%85%D0%BE%D0%B4%D1%8B)
-	[Настройка диаграммы Logging Helm](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%B4%D0%B8%D0%B0%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D1%8B-logging-helm)
    -	[Поддержка Windows](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%BA%D0%B0-windows)
    -	[Работа с пользовательским корневым каталогом Docker](https://github.com/markizz01/test/blob/main/logging/_index.md#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D1%81%D0%BA%D0%B8%D0%BC-%D0%BA%D0%BE%D1%80%D0%BD%D0%B5%D0%B2%D1%8B%D0%BC-%D0%BA%D0%B0%D1%82%D0%B0%D0%BB%D0%BE%D0%B3%D0%BE%D0%BC-docker)
    -	[Работа с пороками и допусками](https://github.com/markizz01/test/blob/main/logging/_index.md#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%B7%D0%B0%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F%D0%BC%D0%B8-%D0%B8-%D0%B4%D0%BE%D0%BF%D1%83%D1%81%D0%BA%D0%B0%D0%BC%D0%B8)
    -	[Ведение журнала V2 с помощью SELinux](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%B0-v2-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E-selinux)
    -	[Дополнительные источники журналов](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%B4%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5-%D0%B8%D1%81%D1%82%D0%BE%D1%87%D0%BD%D0%B8%D0%BA%D0%B8-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%BE%D0%B2)
-	[Исправление проблем](https://github.com/markizz01/test/blob/main/logging/_index.md#%D0%B8%D1%81%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC)


# Включение ведения журнала

Вы можете включить ведение журнала для кластера, управляемого Rancher, перейдя на страницу приложений и установив приложение для ведения журнала.

1.	Перейдите в кластер, где вы хотите установить ведение журнала, и щелкните **Приложения и рынок (Apps & Marketplace)**.
2.	Щелкните приложение **«Ведение журнала».**
3.	Прокрутите до конца диаграммы Helm  до README и нажмите **«Установить»**.
**Результат:** приложение ведения журнала развернуто в cattle-logging-system пространстве имен.

## Удалить ведение журнала

1.	Перейдите в кластер, где вы хотите установить ведение журнала, и щелкните **Приложения и рынок . (Apps & Marketplace).**
2.	Щелкните **Установленные приложения .**
3.	Перейдите в cattle-logging-system пространство имен и установите флажки для rancher-logging и rancher-logging-crd.
4.	Щелкните **Удалить .**
5.	Подтвердите **удаление .**
**Результат:** rancher-logging удален.

# Архитектура

Дополнительные сведения о том, как работает приложение ведения журнала, [см . в этом разделе.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/rbac)

# Управление доступом на основе ролей

Ведение журнала Rancher имеет две роли: logging-admin и logging-view. Дополнительные сведения о том, как и когда использовать эти роли, [см . в этом разделе.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/rbac)

# Настройка журналирования пользовательских ресурсов

Для управления Flows, ClusterFlows, Outputs, и ClusterOutputs

1.	В левом верхнем углу нажмите **☰ > Управление кластером  (Cluster Management).**
2.	На странице **« Кластеры »** перейдите к кластеру, в котором вы хотите настроить ведение журнала пользовательских ресурсов, и нажмите **« Исследовать(Explore) » .**
3.	На левой панели навигации щелкните **Ведение журнала (Logging).**

## Потоки и кластерные потоки

Справку по настройке Flows и ClusterFlows [см . на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/custom-resource-config/flows)

## Выходы и кластерные выходы
Справку по настройке Outputs и ClusterOutputs [см . на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/custom-resource-config/outputs)

# Настройка диаграммы Logging Helm

Список параметров, которые можно настроить при установке или обновлении приложения ведения журнала, [см . на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/helm-chart-options)

## Поддержка Windows

Доступна поддержка ведения журналов для кластеров Windows, и журналы можно собирать с узлов Windows.
Подробнее о том, как включить или отключить ведение журнала узлов Windows, [см . на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/helm-chart-options)

## Работа с пользовательским корневым каталогом Docker

Дополнительные сведения об использовании пользовательского корневого каталога Docker  [см . на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/helm-chart-options)

## Работа с заражениями и допусками

Для получения информации о том, как использовать испорченные данные и допуски с приложением ведения журнала, [см. эту страницу.]( docs/content/rancher/v2.6/en/logging/taints-tolerations/)

## Ведение журнала V2 с помощью SELinux

Для получения информации о включении приложения ведения журнала для узлов с поддержкой SELinux [см . на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/helm-chart-options)

## Дополнительные источники журналов

По умолчанию Rancher собирает журналы для компонентов плоскости управления и узлов для всех типов кластеров. В некоторых случаях могут быть собраны дополнительные журналы. Подробнее [см . на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/helm-chart-options) https://github.com/rancher/docs

# Исправление проблем

## Пространство имен cattle-logging воссоздается

Если ваш кластер ранее развернул ведение журнала из глобального представления в устаревшем пользовательском интерфейсе Rancher, вы можете столкнуться с проблемой, когда его пространство имен cattle-logging постоянно воссоздается.
Решение состоит в том, чтобы удалить все пользовательские ресурсы clusterloggings.management.cattle.io и projectloggings.management.cattle.io из пространства имен конкретного кластера в кластере управления. Существование этих пользовательских ресурсов заставляет Rancher создавать пространство имен cattle-logging в нижестоящем кластере, если оно не существует.
Пространство имен кластера соответствует идентификатору кластера, поэтому нам нужно найти идентификатор кластера для каждого кластера.

1.	В левом верхнем углу нажмите **☰ > Управление кластером (Cluster Management) .**
2.	На странице **« Кластеры »** перейдите к кластеру, идентификатор которого вы хотите получить, и нажмите **« Исследовать( Explore) » .**
3.	Скопируйте часть <cluster-id> одного из URL-адресов ниже. Часть <cluster-id>— это имя пространства имен кластера.
  
```
# Cluster Management UI
https://<your-url>/c/<cluster-id>/

# Cluster Dashboard
https://<your-url>/dashboard/c/<cluster-id>/
```
  
Теперь, когда у нас есть пространство имен <cluster-id>  , мы можем удалить CR, которые вызывают постоянное воссоздание cattle-logging.
Предупреждение: убедитесь, что версия, установленная из устаревшго пользовательского интерфейса Rancher, в настоящее время не используется.
```
kubectl delete clusterloggings.management.cattle.io -n <cluster-id>
kubectl delete projectloggings.management.cattle.io -n <cluster-id>
```
