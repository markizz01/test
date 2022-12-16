


Прочтите это пошаговое руководство Rancher GCP, чтобы быстро развернуть сервер Rancher с подключенным нижестоящим кластером Kubernetes с одной нодой.

Следующие шаги позволят быстро развернуть сервер Rancher на GCP в  single-node (одноузловом) кластере K3s Kubernetes с присоединенным  single-node нисходящим кластером Kubernetes.

**Примечание.** Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Эти руководства не предназначены для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/google-gcp-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/google-gcp-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

**Необходимые условия**

***Внимание*** . За развертывание в Google GCP взимается плата.

- [Учетная запись Google GCP: учетная запись](https://console.cloud.google.com/ "https://console.cloud.google.com/") Google GCP требуется для создания ресурсов для развертывания Rancher и Kubernetes.
- [Проект Google GCP](https://cloud.google.com/appengine/docs/standard/nodejs/building-app/creating-project "https://cloud.google.com/appengine/docs/standard/nodejs/building-app/creating-project") : используйте эту ссылку, чтобы следовать руководству по созданию проекта GCP, если у вас его еще нет.
- [Учетная запись службы Google GCP](https://cloud.google.com/iam/docs/creating-managing-service-account-keys "https://cloud.google.com/iam/docs/creating-managing-service-account-keys") : используйте эту ссылку и следуйте инструкциям, чтобы создать учетную запись службы GCP и файл токена.
- [Terraform](https://www.terraform.io/downloads.html "https://www.terraform.io/downloads.html") : используется для предоставления сервера и кластера в Google GCP.

**Начало работ**

1. Клонируйте [Rancher Quickstart](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") в папку с помощью git clone https://github.com/rancher/quickstart.
1. Перейдите в папку GCP, содержащую файлы terraform, выполнив cd quickstart/rancher/gcp.
1. Переименуйте terraform.tfvars.example в terraform.tfvars.
1. Отредактируйте terraform.tfvars и настройте следующие переменные:
- gcp\_account\_json- Путь и имя файла учетной записи службы GCP.
- rancher\_server\_admin\_password- Пароль администратора для созданного сервера Rancher
1. **Необязательно:** измените необязательные переменные в файлах terraform.tfvars. Дополнительную информацию см. в справочных материалах по [быстрому запуску](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") и в справочных материалах по [быстрому запуску GCP](https://github.com/rancher/quickstart/tree/master/rancher/gcp "https://github.com/rancher/quickstart/tree/master/rancher/gcp") . Предложения включают:
- gcp\_region- Регион Google GCP, выберите ближайший вместо стандартного ( us-east4)
- gcp\_zone- Зона Google GCP, выберите ближайшую вместо стандартной ( us-east4-a)
- prefix- Префикс для всех созданных ресурсов
- machine\_type- Используемый размер компа, минимальный, n1-standard-1, но  может  быть использован n1-standard-2 или n1-standard-4, если предусмотрен бюджет
1. Переходим к  terraform init.
1. Чтобы инициировать создание среды, запустите terraform apply --auto-approve. Затем дождитесь вывода, подобного следующему:



Apply complete! Resources: 16 added, 0 changed, 0 destroyed.



Outputs:



rancher\_node\_ip = xx.xx.xx.xx

rancher\_server\_url = https://rancher.xx.xx.xx.xx.sslip.io

workload\_node\_ip = yy.yy.yy.yy

1. Вставьте rancher\_server\_url из вывода выше в браузер. Войдите в систему, когда будет предложено (имя пользователя по умолчанию admin, используйте пароль, указанный в rancher\_server\_admin\_password).
1. ssh к серверу Rancher, использует  ключ id\_rsa, сгенерированный в quickstart/rancher/gcp.

**Результат**

Два кластера Kubernetes развернуты в вашей учетной записи GCP, один работает под управлением Rancher Server, а другой готов к экспериментальному развертыванию. Обратите внимание, что, несмотря на то, что эта установка является отличным способом изучить функциональность Rancher, производственная установка должна соответствовать нашим рекомендациям по настройке высокой доступности. Ключи SSH для виртуальных машин генерируются автоматически и сохраняются в каталоге модуля.

**Что дальше?**

Используйте Rancher для создания развертывания. Дополнительные сведения см. в разделе  [Creating Deployments]({{< baseurl >}}/rancher/v2.6/en/quick-start-guide/workload).

**Уничтожение ресурсов**

1. Из папки quickstart/rancher/gcp выполнить terraform destroy --auto-approve.
1. Дождитесь подтверждения, что все ресурсы уничтожены.

