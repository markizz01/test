


Прочтите это пошаговое руководство по Rancher Azure, чтобы быстро развернуть сервер Rancher с подключенным нижестоящим кластером Kubernetes с одной нодой.

Следующие шаги позволят быстро развернуть сервер Rancher в Azure в кластере K3s Kubernetes с single-node, к которому подключен нижестоящий кластер Kubernetes с single-node.

**Примечание.** Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Эти руководства не предназначены для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/microsoft-azure-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/microsoft-azure-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

**Необходимые условия**

**Внимание** . За развертывание в Microsoft Azure взимается плата.

- [Учетная запись Microsoft Azure:  учетная запись](https://azure.microsoft.com/en-us/free/ "https://azure.microsoft.com/en-us/free/") Microsoft Azure требуется для создания ресурсов для развертывания Rancher и Kubernetes.
- [Подписка Microsoft Azure](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/create-subscription "https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/create-subscription#create-a-subscription-in-the-azure-portal") . Воспользуйтесь этой ссылкой, чтобы следовать инструкциям по созданию подписки Microsoft Azure, если у вас ее еще нет.
- [Micsoroft Azure Tenant](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-create-new-tenant "https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-create-new-tenant"): : используйте эту ссылку и следуйте инструкциям, чтобы создать арендатора Microsoft Azure.
- [Microsoft Azure Client ID/Secret](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal "https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal"):используйте эту ссылку и следуйте инструкциям, чтобы создать клиента и секрет Microsoft Azure.
- [Terraform](https://www.terraform.io/downloads.html "https://www.terraform.io/downloads.html") : используется для подготовки сервера и кластера в Microsoft Azure.

**Начало работы**

1. Клонируйте [Rancher Quickstart](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") в папку с помощью git clone https://github.com/rancher/quickstart.
1. Перейдите в папку Azure, содержащую файлы terraform, выполнив команду cd quickstart/rancher/azure.
1. Переименуйте terraform.tfvars.example в terraform.tfvars.
1. Отредактируйте terraform.tfvars и настройте следующие переменные:
- azure\_subscription\_id- Идентификатор подписки Microsoft Azure
- azure\_client\_id- идентификатор клиента Microsoft Azure
- azure\_client\_secret- Секрет клиента Microsoft Azure
- azure\_tenant\_id- Идентификатор Microsoft Azure tenant
- rancher\_server\_admin\_password- Пароль администратора для созданного сервера Rancher
1. **Необязательно:** измените необязательные переменные в файлах terraform.tfvars. Дополнительную информацию см. в файлах сведений для [быстрого запуска](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") и в файлах сведений для [быстрого запуска Azure](https://github.com/rancher/quickstart/tree/master/rancher/azure "https://github.com/rancher/quickstart/tree/master/rancher/azure") . Предложения включают:
- azure\_location- Регион Microsoft Azure, выберите ближайший вместо стандартного ( East US)
- prefix- Префикс для всех созданных ресурсов
- instance\_type- Используемый размер Standard\_DS2\_v2, минимальный,  но может  быть использован Standard\_DS2\_v3 или Standard\_DS3\_v2б, если заложен в бюджет
- add\_windows\_node- Если true, в кластер рабочей нагрузки добавляется дополнительный рабочий узел Windows.
- windows\_admin\_password- Пароль администратора рабочего узла Windows
1. Переходим к terraform init.
1. Чтобы инициировать создание среды, запустите terraform apply --auto-approve. Затем дождитесь вывода, подобного следующему:



Apply complete! Resources: 16 added, 0 changed, 0 destroyed.



Outputs:



rancher\_node\_ip = xx.xx.xx.xx

rancher\_server\_url = https://rancher.xx.xx.xx.xx.sslip.io

workload\_node\_ip = yy.yy.yy.yy

1. Вставьте rancher\_server\_url из вывода выше в браузер. Войдите в систему, когда будет предложено (имя пользователя по умолчанию admin, используйте пароль, указанный в rancher\_server\_admin\_password).
1. ssh к серверу Rancher, использует ключ  id\_rsa, сгенерированный в quickstart/rancher/azure.

**Результат**

В вашей учетной записи Azure развернуты два кластера Kubernetes, один из которых работает с сервером Rancher, а другой готов к экспериментальному развертыванию. Обратите внимание, что, несмотря на то, что эта установка является отличным способом изучить функциональность Rancher, производственная установка должна соответствовать нашим рекомендациям по настройке высокой доступности. Ключи SSH для виртуальных машин генерируются автоматически и сохраняются в каталоге модуля.

**Что дальше?**

Используйте Rancher для создания развертывания. Дополнительные сведения см. в разделе [Creating Deployments]({{< baseurl >}}/rancher/v2.6/en/quick-start-guide/workload).

**Уничтожение ресурсов**

1. Из папки quickstart/rancher/azure выполнить terraform destroy --auto-approve.
1. Дождитесь подтверждения, что все ресурсы уничтожены.

