# Интеграция NeuVector в Rancher

Новое в Rancher v2.6.5, [NeuVector 5.x](https://open-docs.neuvector.com/) — это платформа безопасности с открытым исходным кодом, ориентированная на контейнеры, которая теперь интегрирована в Rancher. NeuVector обеспечивает соответствие, прозрачность и защиту критически важных приложений и данных в режиме реального времени во время выполнения. NeuVector предоставляет firewall (брандмауэр), мониторинг контейнеров процессов/файлов системы, аудит безопасности с помощью эталонных тестов CIS (CIS benchmarks ) и сканирование уязвимостей. Дополнительные сведения о безопасности Rancher [см. в документации](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/neuvector-integration/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/security) по безопасности .

NeuVector можно включить с помощью Helm, который можно установить либо через **Apps & Marketplace** , либо с помощью кнопки **Cluster Tools** в пользовательском интерфейсе Rancher. После установки Helm пользователи могут легко [развертывать и управлять кластерами NeuVector в Rancher .](https://open-docs.neuvector.com/deploying/rancher#deploy-and-manage-neuvector-through-rancher-apps-marketplace)

# Установка NeuVector с Rancher

NeuVector Helm Chart используется для управления доступом к пользовательскому интерфейсу NeuVector в Rancher, где пользователи могут напрямую переходить к развертыванию и управлению своими кластерами NeuVector.

## Чтобы перейти к диаграмме NeuVector и установить ее через Apps & Marketplace:

1.	Щелкните **☰ > Cluster Management (Управление кластером) .**
2.	На странице **«Clusters (Кластеры)»** перейдите к кластеру, в котором вы хотите развернуть NeuVector, и нажмите **«Explore (использовать) » .**
3.	Перейдите в раздел **« Apps & Marketplace > Charts»** и установите NeuVector из репозитория диаграмм.
4.	Для разных типов кластеров требуется разное время выполнения. При настройке значений Helm перейдите в раздел **Container Runtime** и выберите свою среду выполнения в соответствии с типом кластера. Наконец, нажмите «Install (Установить) » еще раз.

Вот некоторые примеры:

-	RKE1: docker
-	K3s and RKE2: k3scontainerd
-	AKS: containerd for v1.19 and up
-	EKS: docker for v1.22 and below; containerd for v1.23 and up
-	GKE: containerd (see the [Google docs](https://cloud.google.com/kubernetes-engine/docs/concepts/using-containerd) for more)
**Note:** Only one container runtime engine may be selected at a time during installation.

## Чтобы перейти к диаграмме NeuVector и установить ее с помощью Cluster Tools:

1.	Щелкните **☰ > Cluster Management (Управление кластером) .**
2.	На странице **«Clusters (Кластеры)»** перейдите к кластеру, в котором вы хотите развернуть NeuVector, и нажмите **«Explore (исследовать) .**
3.	Нажмите **« Cluster Tools (Инструменты кластера) »** в нижней части левой панели навигации.
4.	Повторите шаг 4 выше, чтобы соответствующим образом выбрать среду выполнения контейнера, затем снова нажмите **«Install (Установить» .**

## Доступ к NeuVector из пользовательского интерфейса Rancher

1.	Перейдите к обозревателю кластера, где установлен NeuVector. На левой панели навигации щелкните **NeuVector .**
2.	Щелкните внешнюю ссылку, чтобы перейти к пользовательскому интерфейсу NeuVector. После выбора ссылки пользователи должны принять END USER LICENSE AGREEMENT для доступа к пользовательскому интерфейсу NeuVector.

# Удаление NeuVector из пользовательского интерфейса Rancher

## Чтобы удалить из Apps & Marketplace:

1.	Щелкните **☰ > Cluster Management (Управление кластером) .**
2.	В разделе **Apps & Marketplace**, нажмите **Installed Apps. **
3.	В разделе cattle-neuvector-system выберите приложение **NeuVector (и связанный с ним CRD, если необходимо)**, затем нажмите **« Delete (Удалить )» .**

## Чтобы удалить из Cluster Tools:

1.	Щелкните **☰ > Cluster Management (Управление кластером).**
2.	Нажмите **«Cluster Tools  (Инструменты кластера) »** в левом нижнем углу экрана, затем нажмите значок корзины под диаграммой NeuVector. Выберите **Delete the CRD associated with this app**, если хотите, затем нажмите **« Delete (Удалить ).**

# Репозиторий GitHub
Проект NeuVector доступен [здесь.](https://github.com/neuvector/neuvector)

# Документация

Документация NeuVector находится [здесь.](https://open-docs.neuvector.com/)  

# Архитектура

Решение безопасности NeuVector содержит четыре типа контейнеров безопасности: Controllers, Enforcers, Managers, and Scanners (контроллеры, усилители, управляющие элементы и сканеры). Также предоставляется специальный контейнер под названием All-in-One для объединения функций Controller, Enforcer и Manager в одном контейнере, в первую очередь для собственных развертываний Docker. Существует также средство обновления, которое при запуске обновляет базу данных CVE.
-	**Controller:** управляет контейнером NeuVector Enforcer; предоставляет REST APIs для консоли управления.
-	**Enforcer:** Применяет политики безопасности.
-	**Manager:** предоставляет веб-интерфейс и консоль командной строки для управления платформой NeuVector.
-	**All-in-One:** включает Controller, Enforcer и Manager.
-	**Scanner:** выполняет сканирование на уязвимости и соответствие требованиям для изображений, контейнеров и узлов.
-	**Updater:** обновляет базу данных CVE для Neuvector (при запуске); повторно развертывает модули сканера.

**Контейнеры безопасности NeuVector:** 
**NeuVector Architecture:** 

Чтобы узнать больше об архитектуре NeuVector, обратитесь [сюда.](https://open-docs.neuvector.com/basics/overview#architecture)

# Распределение ЦП и памяти

Ниже приведены минимальные рекомендуемые вычислительные ресурсы для установки NeuVector в развертывании по умолчанию. Обратите внимание, что лимит ресурсов не установлен.

|Container	|CPU - Request	|Memory - Request|
|:-|:-|:-|
|Controller	|3 (1GB 1vCPU needed per controller)	|* |
|Enforcer	|On all nodes (500MB .5vCPU)	|1GB|
|Manager	|1 (500MB .5vCPU)	|* |
|Scanner	|3 (100MB .5vCPU)	|* |

* Для контейнеров Controller, Manager и Scanner вместе взятые требуется минимум 1 ГБ памяти.
Усиленная поддержка кластеров — Calico и Canal*

-	Все компоненты NeuVector можно развертывать, если для PSP установлено значение true.

# *Новое в версии 2.6.7*

Вам потребуется установить дополнительную конфигурацию для защищенной кластерной среды следующим образом:
1.	Щелкните **☰ >  Cluster Management (Управление кластером) .**
2.	Перейдите к созданному вами кластеру и нажмите **Explore (Исследовать) .**
3.	На левой панели навигации щелкните **Apps & Marketplace.**
4.	Установите (или обновите) версию NeuVector 100.0.1+up2.2.2.
    -	В разделе **Edit Options > Other Configuration** включите **Pod Security Policy** , установив флажок (другая конфигурация не требуется):
https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/neuvector-integration/%7B%7B%3Cbaseurl%3E%7D%7D/img/rancher/psp-nv-rke.png 
5.	Нажмите « Install (Установить)» в правом нижнем углу для завершения.
	
-	Компоненты NeuVector Controller и Enforcer можно развернуть, если для PSP установлено значение true.

**Применимо только к версии NeuVector 100.0.0+up2.2.0:**

-	Для компонентов Manager, Scanner и Updater требуется дополнительная настройка, как показано ниже:
```
kubectl patch deploy neuvector-manager-pod -n cattle-neuvector-system --patch '{"spec":{"template":{"spec":{"securityContext":{"runAsUser": 5400}}}}}' 
kubectl patch deploy neuvector-scanner-pod -n cattle-neuvector-system --patch '{"spec":{"template":{"spec":{"securityContext":{"runAsUser": 5400}}}}}'
kubectl patch cronjob neuvector-updater-pod -n cattle-neuvector-system --patch '{"spec":{"jobTemplate":{"spec":{"template":{"spec":{"securityContext":{"runAsUser": 5400}}}}}}}'
```

# *Новое в версии 2.6.7*

Вам потребуется установить дополнительную конфигурацию для защищенной кластерной среды.

*Примечание. Вы должны обновить свою конфигурацию в защищенных кластерах RKE2 и K3s, как показано ниже.*

1.	Щелкните **☰ > Cluster Management (Управление кластером) .**
2.	Перейдите к созданному вами кластеру и нажмите **Explore (Исследовать) .**
3.	На левой панели навигации щелкните **Apps & Marketplace.**
4.	Установите (или обновите) версию NeuVector 100.0.1+up2.2.2.
    -	В разделе **« Edit Options > Other Configuration(Параметры редактирования » > « Другая конфигурация) »** включите **Pod Security Policy (политику безопасности )**, установив флажок. Обратите внимание, что вы также должны ввести значение больше, чем zero для Manager runAsUser ID, Scanner runAsUser IDи Updater runAsUser ID:
 https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/neuvector-integration/%7B%7B%3Cbaseurl%3E%7D%7D/img/rancher/psp-nv-rke2.png 
5.	Нажмите « Install (Установить)» в правом нижнем углу для завершения.
 
## Поддержка кластеров с поддержкой SELinux — Calico и Canal

Чтобы включить SELinux в кластерах RKE2, выполните следующие действия:
-	Компоненты NeuVector Controller и Enforcer можно развернуть, если для PSP установлено значение true.

**Применимо только к версии диаграммы NeuVector 100.0.0+up2.2.0:**
-	Для компонентов Manager, Scanner и Updater требуется дополнительная настройка, как показано ниже:
```
kubectl patch deploy neuvector-manager-pod -n cattle-neuvector-system --patch '{"spec":{"template":{"spec":{"securityContext":{"runAsUser": 5400}}}}}'
kubectl patch deploy neuvector-scanner-pod -n cattle-neuvector-system --patch '{"spec":{"template":{"spec":{"securityContext":{"runAsUser": 5400}}}}}'
kubectl patch cronjob neuvector-updater-pod -n cattle-neuvector-system --patch '{"spec":{"jobTemplate":{"spec":{"template":{"spec":{"securityContext":{"runAsUser": 5400}}}}}}}'
```

# Поддержка кластера в изолированной среде

-	Все компоненты NeuVector можно развернуть на кластере в изолированной среде без дополнительной настройки.

# Ограничения поддержки
-	В настоящее время поддерживаются только администраторы и владельцы кластеров.
-	Многокластерное развертывание Fleet не поддерживается.
-	NeuVector не поддерживается в кластере Windows.

# Другие ограничения
-	В настоящее время установка NeuVector завершается сбоем, если партнерская диаграмма NeuVector уже существует. Чтобы обойти эту проблему, удалите партнерскую NeuVector и переустановите NeuVector.
-	Иногда, когда контроллеры не готовы, пользовательский интерфейс NeuVector недоступен из пользовательского интерфейса Rancher. В течение этого времени контроллеры попытаются перезапуститься, и потребуется несколько минут, чтобы контроллеры стали активными.
-	Время выполнения контейнера не определяется автоматически для разных типов кластеров при установке диаграммы NeuVector. Чтобы обойти это, вы можете указать время выполнения вручную.
