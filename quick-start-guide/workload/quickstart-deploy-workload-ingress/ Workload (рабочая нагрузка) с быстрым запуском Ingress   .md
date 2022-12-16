

**Необходимое условие**

У вас есть работающий кластер как минимум с 1 нодой.

**1. Развертывание Workload (рабочей нагрузки)**

**Вы готовы создать свой первый Workload Kubernetes . Workload**

— это объект, который включает модули вместе с другими файлами и информацией, необходимой для развертывания вашего приложения.

Для этой рабочей нагрузки вы будете развертывать приложение Rancher Hello-World.

1. Щелкните **☰ > Cluster Management (Управление кластером)** .
1. Перейдите к созданному вами кластеру и нажмите **Explore (Исследовать)** .
1. Щелкните **Workload** (**Рабочая нагрузка)** .
1. Щелкните **Create** (**Создать)** .
1. Щелкните **Deployment (Развертывание)**.
1. Введите **Name имя** для вашей рабочей нагрузки.
1. Из поля « **Docker Image- Образ Docker** » введите rancher/hello-world. Это поле учитывает регистр.
1. Нажмите « **Add Port -Добавить порт»** и введите 80в поле «**Private Container Port -**  **Порт частного контейнера»** . Добавление порта обеспечивает доступ к приложению внутри и за пределами кластера. Дополнительные сведения см. в разделе [Услуги](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/workloads/ "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/workloads/#services") .
1. Щелкните **Create - Создать** .

**Результат:**

- Ваша рабочая нагрузка развернута. Этот процесс может занять несколько минут.
- Когда ваша рабочая нагрузка завершает развертывание, ей присваивается состояние **Active** . Вы можете просмотреть этот статус на странице **Workloads -** **рабочих нагрузок** проекта .


` `### 2. Откройте приложение через Ingress

Теперь, когда приложение запущено и работает, его необходимо открыть, чтобы другие службы могли подключиться.

1. Щелкните **☰ > Управление кластером** .
1. Перейдите к созданному вами кластеру и нажмите **Исследовать** .
1. Нажмите **Service Discovery > Ingresses  - «Обнаружение служб» > «Входы»** .
1. Щелкните **Создать.**
1. При выборе **Namespace - пространства имен** убедитесь, что оно совпадает с тем, которое использовалось при создании развертывания. В противном случае ваше развертывание будет недоступно, когда вы попытаетесь выбрать **Target Service** , как на шаге 8 ниже.
1. Введите **имя** , например **hello - привет** .
1. Укажите свой **Path -** **путь** , например /hello.
1. В поле « **Target Service - Целевая служба** » раскройте список и выберите имя, которое вы установили для своей службы.
1. В поле **Port -** **Порт** раскройте список и выберите 80.
1. Нажмите **Create - Создать** в правом нижнем углу.

**Результат:** приложению назначается  адрес sslip.io и оно открывается. Заполнение может занять минуту или две.

**Просмотр вашего приложения**

На странице «**Deployments -** **Развертывания »** найдите столбец **«Endpoints - Конечные точки** » для вашего развертывания и щелкните конечную точку. Доступные конечные точки будут зависеть от того, как вы настроили порт, добавленный в развертывание. Для конечных точек, где вы не видите случайно назначенный порт, добавьте путь, который вы указали при создании входа, к IP-адресу. Например, если ваша конечная точка выглядит так xxx.xxx.xxx.xxx или [https://xxx.xxx.xxx.xxx](https://xxx.xxx.xxx.xxx/ "https://xxx.xxx.xxx.xxx") поменяйте ее на xxx.xxx.xxx.xxx/hello или https://xxx.xxx.xxx.xxx/hello.

Ваше приложение откроется в отдельном окне.

**Окончание**

Поздравляем! Вы успешно развернули рабочую нагрузку, доступную через вход.

**Что дальше?**

Когда вы закончите использовать свою песочницу, уничтожьте сервер Rancher и ваш кластер. См. одно из следующего:

- [Amazon AWS: уничтожение](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/ "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/#destroying-the-environment") ресурсов
- [DigitalOcean: уничтожение ресурсов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/ "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/#destroying-the-environment")
- [Vagrant: уничтожение](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/ "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/#destroying-the-environment") ресурса

