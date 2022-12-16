


Следующие шаги позволяют быстро развернуть сервер Rancher с подключенным кластером одной ноды.

***Примечание.*** Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Эти руководства не предназначены для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

**Необходимые условия**

- [Vagrant](https://www.vagrantup.com/ "https://www.vagrantup.com/") : требуется Vagrant, так как он используется для подготовки машины на основе Vagrantfile.
- [Virtualbox](https://www.virtualbox.org/ "https://www.virtualbox.org/") : виртуальные машины, которые Vagrant предоставляет, должны быть предоставлены VirtualBox.
- Не менее 4 ГБ свободной оперативной памяти.

***Примечание***

- Vagrant потребуются плагины для создания виртуальных машин VirtualBox. Установите их с помощью следующих команд:

vagrant plugin install vagrant-vboxmanage

vagrant plugin install vagrant-vbguest

**Начало работы**

1. Клонируйте [Rancher Quickstart](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") в папку с помощью git clone https://github.com/rancher/quickstart.
1. Перейдите в папку, содержащую Vagrantfile, выполнив cd quickstart/rancher/vagrant.
1. **Необязательно:** изменить config.yamlна:
- При необходимости измените количество узлов и распределение памяти. ( node.count, node.cpus, node.memory)
- Сменить пароль admin пользователя для входа в Rancher. ( admin\_password)
1. Чтобы инициировать создание среды, запустите vagrant up --provider=virtualbox.
1. После завершения подготовки перейдите https://192.168.56.101в браузере. Пользователь/пароль по умолчанию admin/adminPassword.

**Результат:** Rancher Server и ваш кластер Kubernetes установлены на VirtualBox.

**Что дальше?**

Используйте Rancher для создания развертывания. Дополнительные сведения см. в разделе [Создание развертываний](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload") .

**Уничтожение ресурсов**

1. Из папки quickstart/rancher/vagrant выполнить vagrant destroy -f.
1. Дождитесь подтверждения, что все ресурсы уничтожены.

