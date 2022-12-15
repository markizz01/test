||||
|:-|:-|:-|
|Rancher-Logting Параметры диаграммы Helm|||

-	[Включить/отключить ведение журнала узла Windows](https://github.com/markizz01/test/blob/main/logging/helm-chart-options/_index.md#%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C%D0%BE%D1%82%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C-%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%B0-%D1%83%D0%B7%D0%BB%D0%B0-windows)
-	[Работа с пользовательским корневым каталогом Docker](https://github.com/markizz01/test/blob/main/logging/helm-chart-options/_index.md#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D1%81%D0%BA%D0%B8%D0%BC-%D0%BA%D0%BE%D1%80%D0%BD%D0%B5%D0%B2%D1%8B%D0%BC-%D0%BA%D0%B0%D1%82%D0%B0%D0%BB%D0%BE%D0%B3%D0%BE%D0%BC-docker)
-	[Добавление настроек NodeSelector и допусков для пользовательских Taints](https://github.com/markizz01/test/blob/main/logging/helm-chart-options/_index.md#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BA-nodeselector-%D0%B8-%D0%B4%D0%BE%D0%BF%D1%83%D1%81%D0%BA%D0%BE%D0%B2-%D0%B4%D0%BB%D1%8F-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D1%81%D0%BA%D0%B8%D1%85-taints)
-	[Включение приложения ведения журнала для работы с SELinux](https://github.com/markizz01/test/blob/main/logging/helm-chart-options/_index.md#%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%B0-%D0%B4%D0%BB%D1%8F-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-%D1%81-selinux)
-	[Дополнительные источники журналов](https://github.com/markizz01/test/blob/main/logging/helm-chart-options/_index.md#%D0%B4%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5-%D0%B8%D1%81%D1%82%D0%BE%D1%87%D0%BD%D0%B8%D0%BA%D0%B8-%D0%B6%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%BE%D0%B2)
-	[Конфигурация системы](https://github.com/markizz01/test/blob/main/logging/helm-chart-options/_index.md#%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B)


## Включить/отключить ведение журнала узла Windows

Вы можете включить или отключить ведение журнала узлов Windows, установив global.cattle.windows.enabled для любого true или false в файле values.yaml.

По умолчанию ведение журнала узлов Windows будет включено, если пользовательский интерфейс Cluster Dashboard используется для установки приложения ведения журнала в кластере Windows.

При данном сценарии установка global.cattle.windows.enabled в false отключит ведение журнала узлов Windows в кластере. Если этот параметр отключен, журналы по-прежнему будут собираться с узлов Linux в кластере Windows.

***Примечание:** В настоящее время существует проблема , из-за которой nodeAgents узла Windows не удаляются при выполнении helm upgrade после отключения ведения журнала Windows в кластере Windows. В этом сценарии пользователям может потребоваться вручную удалить nodeAgents узлов Windows, если они уже установлены.*

## Работа с пользовательским корневым каталогом Docker

Если вы используете собственный корневой каталог Docker, вы можете установить global.dockerRootDirectory в values.yaml.

Это гарантирует, что созданные CR ведения журнала вероятнее всего будут использовать указанный вами путь, а не по умолчанию  Docker в расположении data-root.

Обратите внимание, что это влияет только на узлы Linux.

Если в кластере есть какие-либо узлы Windows, изменение не будет применяться к этим узлам.

## Добавление настроек NodeSelector и допусков для пользовательских Taints

Вы можете добавить свои собственные nodeSelector настройки и добавить tolerations для дополнительных настроек, отредактировав значения диаграммы Helm для регистрации. Подробнее [см . на этой странице. docs/content/rancher/v2.6/en/logging/taints-tolerations/ ](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/taints-tolerations)

## Включение приложения ведения журнала для работы с SELinux

**Требования:** ведение журнала v2 было протестировано с помощью SELinux на RHEL/CentOS 7 и 8.

[Security-Enhanced Linux (SELinux)](https://en.wikipedia.org/wiki/Security-Enhanced_Linux) — это усовершенствованная система безопасности Linux. Поскольку SELinux исторически использовался государственными учреждениями, теперь он является отраслевым стандартом и включен по умолчанию в CentOS 7 и 8.

Чтобы использовать Logging v2 с SELinux, мы рекомендуем установить rancher-selinuxRPM в соответствии с инструкциями на этой странице. https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/logging/helm-chart-options/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/security/selinux/.

Затем при установке приложения ведения журнала настройте диаграмму так, чтобы она поддерживала SELinux, изменив global.seLinux.enabled на true в файле values.yaml.

## Дополнительные источники журналов

По умолчанию Rancher собирает журналы для компонентов плоскости управления https://kubernetes.io/docs/concepts/overview/components/#control-plane-components  и узлов https://kubernetes.io/docs/concepts/overview/components/#node-components  для всех типов кластеров.

В некоторых случаях Rancher может собирать дополнительные журналы.

В следующей таблице приведены источники, из которых могут собираться дополнительные журналы для каждого типа узлов:

|Источник регистрации|Узлы Linux (в том числе в кластере Windows)|Узлы Windows|
|:-|:-|:-|
|РКЭ	|✓	|✓ |
|РКЭ2	|✓	|  |
|К3с	|✓	|   |
|АКС	|✓	|   |
|ЭКС	|✓	|   |
|ГКЭ	|✓	|   |
 
Чтобы включить размещенных провайдеров Kubernetes в качестве дополнительных источников ведения журнала, установите флажок **Включить расширенное ведение журнала облачного провайдера** при установке или обновлении диаграммы Logging Helm.

Если этот параметр включен, Rancher собирает все дополнительные журналы узлов и плоскостей управления, предоставленные провайдером, которые могут различаться в зависимости от провайдера.

Если вы уже используете собственное решение для ведения журналов от облачного провайдера, такое как AWS CloudWatch или Google Cloud Operations Suite (ранее Stackdriver), нет необходимости включать этот параметр, поскольку собственное решение будет иметь неограниченный доступ ко всем журналам.

## Конфигурация системы

В журнале Rancher SystemdLogPath должен быть настроен для дистрибутивов K3s и RKE2 Kubernetes.

Дистрибутивы K3s и RKE2 Kubernetes ведут журнал в journald, который является подсистемой systemd, используемой для ведения журнала. Чтобы собрать эти журналы, systemdLogPath необходимо определить. Хотя каталог run/log/journal используется по умолчанию, некоторые дистрибутивы Linux не используют этот путь по умолчанию. Например, Ubuntu по умолчанию использует var/log/journal. Чтобы определить вашу конфигурацию systemdLogPath, см. шаги ниже.

**Шаги для настройки Systemd:**

-	Запустите cat /etc/systemd/journald.conf | grep -E ^\#?Storage | cut -d"=" -f2на одном из ваших узлов.
-	Если persistent возвращается, ваш systemdLogPath должен быть /var/log/journal.
-	Если volatile возвращается, ваш systemdLogPath должен быть /run/log/journal.
-	Если auto возвращается, проверьте, существует ли /var/log/journal.
    +	Если /var/log/journal существует, то используйте /var/log/journal.
    +	Если /var/log/journal не существует, то используйте /run/log/journal.


***Примечание:** Если возвращается какое-либо значение, не описанное выше, Rancher Logging не сможет собирать журналы уровня управления. Чтобы решить эту проблему, вам потребуется выполнить следующие действия на каждом узле плоскости управления:*
-	Установить Storage=volatile в journald.conf.
-	Перезагрузите устройство.
- Установите systemdLogPath на /run/log/journal.
