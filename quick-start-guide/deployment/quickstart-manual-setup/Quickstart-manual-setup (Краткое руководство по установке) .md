
Быстрый запуск Helm CLI 

В этих инструкциях описывается быстрый способ установки экспериментальной установки Rancher.

В этих инструкциях предполагается, что у вас есть виртуальная машина Linux, с которой вы будете взаимодействовать с локальной рабочей станции. Rancher будет установлен на машине с Linux. Вам нужно будет получить IP-адрес этой машины, чтобы вы могли получить доступ к Rancher с вашей локальной рабочей станции. Rancher предназначен для удаленного управления кластерами Kubernetes, поэтому любой кластер Kubernetes, которым Rancher будет управлять в будущем, также должен иметь доступ к этому IP-адресу.

Мы не рекомендуем устанавливать Rancher локально, потому что это создает проблемы с сетью. Установка Rancher на локальном хосте не позволяет Rancher взаимодействовать с нижестоящими кластерами Kubernetes, поэтому на локальном хосте вы не сможете протестировать функции подготовки кластера Rancher или управления кластером.

Ваше устройство с Linux может быть где угодно. Это может быть Amazon EC2 instance, Digital Ocean droplet или виртуальная машина Azure, если назвать несколько примеров. Другие документы Rancher часто используют термин «нода» как общий термин для всего этого. Один из возможных способов развернуть компьютер с Linux — настроить экземпляр Amazon EC2, как показано в [этом руководстве](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/resources/k8s-tutorials/infrastructure-tutorials/ec2-node "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/resources/k8s-tutorials/infrastructure-tutorials/ec2-node") .

Полные требования к установке [здесь](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/requirements "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/requirements") .  <https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/requirements> 

**Установите K3s в Linux**

Установите кластер K3s, выполнив эту команду на компьютере с Linux:

curl -sfL https://get.k3s.io | INSTALL\_K3S\_VERSION="\*\*\*" sh -s - server --cluster-init

Rancher необходимо установить на поддерживаемую версию Kubernetes. Чтобы указать версию K3s, используйте переменную среды INSTALL\_K3S\_VERSION при запуске сценария установки K3s. См . [условия обслуживания поддержки](https://rancher.com/support-maintenance-terms/ "https://rancher.com/support-maintenance-terms/") .

Использование --cluster-init позволяет K3s использовать встроенный etcd в качестве хранилища данных и имеет возможность конвертировать в настройку высокой доступности. См . раздел [Высокая доступность со встроенной базой данных](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/k3s/latest/en/installation/ha-embedded "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/k3s/latest/en/installation/ha-embedded") .

Сохраните IP-адрес Linux устройства.

**Сохраните kubeconfig на своей рабочей станции.**

Файл kubeconfig важен для доступа к кластеру Kubernetes. Скопируйте файл /etc/rancher/k3s/k3s.yaml с компьютера с Linux и сохраните его на локальной рабочей станции в каталоге ~/.kube/config. Один из способов сделать это — использовать scp инструмент scp и запустить эту команду на локальном компьютере:

{{% tabs %}} {{% tab "Mac and Linux" %}} 



scp root@<IP\_OF\_LINUX\_MACHINE>:/etc/rancher/k3s/k3s.yaml ~/.kube/config



{{% /tab %}} {{% tab "Windows" %}} 

По умолчанию «scp» не является распознаваемой командой, поэтому сначала нам нужно установить модуль.

В Windows PowerShell:

Find-Module Posh-SSH

Install-Module Posh-SSH



\## Get the remote kubeconfig file

scp root@<IP\_OF\_LINUX\_MACHINE>:/etc/rancher/k3s/k3s.yaml $env:USERPROFILE\.kube\config

{{% /tab %}} {{% /tabs %}}** 

**Отредактируйте URL-адрес сервера Rancher в kubeconfig.**

В файле kubeconfig вам нужно будет изменить значение поля server на <IP\_OF\_LINUX\_NODE>:6443. API-сервер Kubernetes будет доступен через порт 6443, а сервер Rancher — через порты 80 и 443. Это редактирование необходимо, чтобы при запуске команд Helm или kubectl с локальной рабочей станции вы могли взаимодействовать с Кластер Kubernetes, на котором будет установлен Rancher.



{{% tabs %}} {{% tab "Mac and Linux" %}} 

Один из способов открыть файл kubeconfig для редактирования — использовать Vim:

vi ~/.kube/config

Нажмите i, чтобы перевести Vim в режим вставки. Чтобы сохранить работу, нажмите Esc. Затем нажмите :wq и нажмите Enter.



{{% /tab %}} {{% tab "Windows" %}} 



В Windows Powershell вы можете использовать notepad.exe для редактирования файла kubeconfig:

notepad.exe $env:USERPROFILE\.kube\config



После редактирования нажмите ctrl+s или перейдите, File > Save чтобы сохранить свою работу.

{{% /tab %}} {{% /tabs %}}** 

**Установите Rancher с Helm**

Затем с вашей локальной рабочей станции выполните следующие команды. Вам понадобятся установленые kubectl и helm. .

helm repo add rancher-latest https://releases.rancher.com/server-charts/latest



kubectl create namespace cattle-system



kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.7.1/cert-manager.crds.yaml



helm repo add jetstack https://charts.jetstack.io



helm repo update



helm install cert-manager jetstack/cert-manager \

`  `--namespace cert-manager \

`  `--create-namespace \

`  `--version v1.7.1



\# Windows Powershell

helm install cert-manager jetstack/cert-manager `

`  `--namespace cert-manager `

`  `--create-namespace `

`  `--version v1.7.1



Последняя команда для установки Rancher приведена ниже. Команде требуется доменное имя, которое перенаправляет трафик на компьютер с  Linux. Для простоты в этом руководстве вы можете использовать поддельное доменное имя для создания своего proof-of-concept (проверки концепции). Примером поддельного доменного имени может быть <IP\_OF\_LINUX\_NODE>.sslip.io.

Чтобы установить конкретную версию Rancher, используйте флаг –version (например, --version 2.6.6). В противном случае по умолчанию устанавливается последняя версия Rancher. См . [Выбор версии Rancher](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/resources/choosing-version "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/resources/choosing-version") .



helm install rancher rancher-latest/rancher \

`  `--namespace cattle-system \

`  `--set hostname=<IP\_OF\_LINUX\_NODE>.sslip.io \

`  `--set replicas=1 \

`  `--set bootstrapPassword=<PASSWORD\_FOR\_RANCHER\_ADMIN>



\# Windows Powershell

helm install rancher rancher-latest/rancher `

`  `--namespace cattle-system `

`  `--set hostname=<IP\_OF\_LINUX\_NODE>.sslip.io `

`  `--set replicas=1 `

`  `--set bootstrapPassword=<PASSWORD\_FOR\_RANCHER\_ADMIN>



Теперь, если вы перейдете <IP\_OF\_LINUX\_NODE>.sslip.io в веб-браузере, вы должны увидеть пользовательский интерфейс Rancher.

Чтобы упростить эти инструкции, мы использовали поддельное доменное имя и самозаверяющие сертификаты для этой установки. Поэтому вам, вероятно, потребуется добавить исключение безопасности в веб-браузер, чтобы увидеть пользовательский интерфейс Rancher. Обратите внимание, что для производственных установок вам потребуется настройка высокой доступности с load balancer (балансировщиком нагрузки), реальным доменным именем и настоящими сертификатами.

В этих инструкциях также не указаны полные требования к установке и другие параметры установки. Если у вас возникли проблемы с этими шагами, обратитесь к полной [документации по установке Helm CLI.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/install-rancher-on-k8s "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/install-rancher-on-k8s")

Чтобы запустить новые кластеры Kubernetes с вашим новым сервером Rancher, вам может потребоваться настроить облачные учетные данные в Rancher. Дополнительные сведения см. в разделе [Запуск кластеров Kubernetes с помощью Rancher.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning/rke-clusters "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-manual-setup/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning/rke-clusters")
