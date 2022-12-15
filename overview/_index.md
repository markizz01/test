Rancher — это платформа управления контейнерами, созданная для организаций, развертывающих контейнеры в производственной среде. Rancher позволяет легко запускать Kubernetes где угодно, соответствовать ИТ-требованиям и расширять возможности команд DevOps.

# Запускайте Kubernetes везде

Kubernetes стал стандартом оркестрации контейнеров. Большинство поставщиков облачных услуг и средств виртуализации теперь предлагают его в качестве стандартной инфраструктуры. Пользователи Rancher могут создавать кластеры Kubernetes с помощью Rancher Kubernetes Engine (RKE) или облачных сервисов Kubernetes, таких как GKE, AKS и EKS. Пользователи Rancher также могут импортировать свои существующие кластеры Kubernetes, созданные с помощью любого дистрибутива или установщика Kubernetes, и управлять ими.

# Соответствие ИТ-требованиям

Rancher поддерживает централизованную аутентификацию, контроль доступа и мониторинг для всех кластеров Kubernetes, находящихся под его контролем. Например, вы можете:
-	Использовать свои учетные данные Active Directory для доступа к кластерам Kubernetes, размещенным у поставщиков облачных услуг, таких как GKE.
-	Настроить и применять политики контроля доступа и безопасности для всех пользователей, групп, проектов, кластеров и облаков.
-	Просматривать работоспособность и емкость кластеров Kubernetes из единого окна.

# Расширение возможностей команд DevOps

Rancher предоставляет инженерам DevOps интуитивно понятный пользовательский интерфейс для управления рабочей нагрузкой своих приложений. Пользователю не нужно иметь глубокие знания концепций Kubernetes, чтобы начать использовать Rancher. Каталог Rancher содержит набор полезных инструментов DevOps. Rancher сертифицирован для широкого спектра продуктов облачной экосистемы, включая, например, инструменты безопасности, системы мониторинга, реестры контейнеров, а также драйверы для хранения и сети.
На следующем рисунке показана роль Rancher в организациях, занимающихся ИТ и DevOps. Каждая команда развертывает свои приложения в публичном или частном облаке по своему выбору. ИТ-администраторы получают видимость и применяют политики для всех пользователей, кластеров и облаков.
![pic](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/img/rancher/platform.png)

# Возможности API-сервера Rancher

Сервер API Rancher построен на основе встроенного сервера API Kubernetes и базы данных etcd. Он реализует следующие функции:

## Авторизация и управление доступом на основе ролей
-	**Управление пользователями:** сервер Rancher API [управляет удостоверениями пользователей](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/authentication) , которые соответствуют внешним поставщикам аутентификации, таким как Active Directory или GitHub, в дополнение к локальным пользователям.
-	**Авторизация:** Сервер Rancher API управляет [контролем доступа](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/rbac) и [политиками безопасности.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/pod-security-policies)
## Работа с Кубернетом
-	**Инициализация кластеров Kubernetes:** сервер Rancher API может [инициализировать Kubernetes](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning) на существующих нодах или выполнять [обновления Kubernetes.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-admin/upgrading-kubernetes)
-	**Управление каталогом:** Rancher предоставляет возможность использовать [каталог чартов Helm](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/helm-charts) , которые упрощают многократное развертывание приложений.
-	**Управление проектами.** Проект — это группа из нескольких пространств имен и политик управления доступом в кластере. Проект — это концепция Rancher, а не концепция Kubernetes, которая позволяет вам управлять несколькими пространствами имен как группой и выполнять в них операции Kubernetes. Пользовательский интерфейс Rancher предоставляет функции для [администрирования проектов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin) и [управления приложениями в проектах.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher)
-	**Конвейеры.** Настройка [конвейера](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/pipelines) может помочь разработчикам выпускать новое программное обеспечение максимально быстро и эффективно. В Rancher вы можете настроить конвейеры для каждого из ваших проектов Rancher.
-	**Istio:** наша [интеграция с Istio](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/istio) разработана таким образом, чтобы оператор Rancher, например администратор или владелец кластера, мог предоставлять Istio разработчикам. Затем разработчики могут использовать Istio для обеспечения соблюдения политик безопасности, устранения неполадок или управления трафиком для зеленых/синих развертываний, канареечных развертываний или A/B-тестирования.

# Работа с облачной инфраструктурой
-	Отслеживание нодов. Сервер Rancher API отслеживает идентификаторы всех [нодов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-admin/nodes) во всех кластерах.
-	Настройка инфраструктуры: при настройке на использование облачного провайдера Rancher может динамически выделять [новые ноды](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning/rke-clusters/node-pools) и [постоянное хранилище](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-admin/volumes-and-storage) в облаке.

# Доступность(прозрачность) кластера
-	**Ведение журнала:** Rancher может интегрироваться с различными популярными службами и инструментами ведения журнала, которые существуют за пределами ваших кластеров Kubernetes.
-	**Мониторинг:** с помощью Rancher вы можете отслеживать состояние и процессы нодов вашего кластера, компонентов Kubernetes и развертываний программного обеспечения благодаря интеграции с Prometheus, ведущим решением для мониторинга с открытым исходным кодом.
-	**Оповещение.** Чтобы поддерживать работоспособность кластеров и приложений и повышать производительность вашей организации, вам необходимо быть в курсе событий, происходящих в ваших кластерах и проектах, как запланированных, так и незапланированных.

# Редактирование нижестоящих кластеров с помощью Rancher
Параметры и настройки, доступные для существующего кластера, изменяются в зависимости от метода, который вы использовали для его подготовки. Например, только кластеры, [предоставленные RKE](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning/rke-clusters) , имеют Cluster Options  (параметры кластера) , доступные для редактирования.
После создания кластера с помощью Rancher администратор кластера может управлять членством в кластере, включать политики безопасности модулей и управлять пулами нодов, а [также другими параметрами](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-admin/editing-clusters).
В следующей таблице приведены все параметры и настройки, доступные для каждого типа кластера.


