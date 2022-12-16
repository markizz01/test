

Прочитайте это пошаговое руководство Rancher Hetzner Cloud, чтобы быстро развернуть сервер Rancher с подключенным нижестоящим кластером Kubernetes с одной нодой.

Следующие шаги позволят быстро развернуть сервер Rancher в облаке Hetzner в single-node (одноузловом)кластере K3s Kubernetes с присоединенным single-node нисходящим кластером Kubernetes.

**Примечание.** Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Эти руководства не предназначены для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/hetzner-cloud-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/hetzner-cloud-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

**Необходимые условия**

***Внимание*** . За развертывание в Hetzner Cloud взимается плата.

- [Облачная учетная запись Hetzner](https://www.hetzner.com/ "https://www.hetzner.com/") : вам потребуется учетная запись в Hetzner, так как именно здесь будут работать сервер и кластер.
- [Ключ доступа к Hetzner API](https://docs.hetzner.cloud/ "https://docs.hetzner.cloud/#getting-started") : используйте эти инструкции для создания ключа Hetzner Cloud API, если у вас его нет.
- [Terraform](https://www.terraform.io/downloads.html "https://www.terraform.io/downloads.html") : используется для предоставления сервера и кластера Hetzner.

**Начало работы**

1. Клонируйте [Rancher Quickstart](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") в папку с помощью git clone https://github.com/rancher/quickstart.
1. Перейдите в папку Hetzner, содержащую файлы terraform, выполнив cd quickstart/rancher/hcloud.
1. Переименуйте terraform.tfvars.example в terraform.tfvars.
1. Отредактируйте terraform.tfvars и настройте следующие переменные:
- hcloud\_token- Ключ доступа к API Hetzner
- rancher\_server\_admin\_password- Пароль администратора для созданного сервера Rancher
1. **Необязательно:** измените необязательные переменные в файлах terraform.tfvars. Для получения дополнительной информации см . и ознакомительные сведения о [быстром запуске ](https://github.com/rancher/quickstart/tree/master/rancher/hcloud "https://github.com/rancher/quickstart/tree/master/rancher/hcloud")[Hetzner](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") . Предложения включают:
- prefix- Префикс для всех созданных ресурсов
- instance\_type- Тип экземпляра, минимум требуется cx21
- hcloud\_location- Местоположение Hetzner Cloud, выберите ближайшее вместо значения по умолчанию ( fsn1)
1. Переходим к terraform init.
1. Чтобы инициировать создание среды, запустите terraform apply --auto-approve. Затем дождитесь вывода, подобного следующему:



Apply complete! Resources: 15 added, 0 changed, 0 destroyed.



Outputs:



rancher\_node\_ip = xx.xx.xx.xx

rancher\_server\_url = https://rancher.xx.xx.xx.xx.sslip.io

workload\_node\_ip = yy.yy.yy.yy

1. Вставьте rancher\_server\_url из вывода выше в браузер. Войдите в систему, когда будет предложено (имя пользователя по умолчанию admin, используйте пароль, указанный в rancher\_server\_admin\_password).
1. ssh к серверу Rancher использует ключ id\_rsa, сгенерированный в quickstart/rancher/hcloud.

**Результат**

Два кластера Kubernetes развернуты в вашей учетной записи Hetzner, один работает под управлением Rancher Server, а другой готов к экспериментальному развертыванию. Обратите внимание, что, несмотря на то, что эта установка является отличным способом изучить функциональность Rancher, производственная установка должна соответствовать нашим рекомендациям по настройке высокой доступности. Ключи SSH для виртуальных машин генерируются автоматически и сохраняются в каталоге модуля.

**Что дальше?**

Используйте Rancher для создания развертывания. Дополнительные сведения см. в разделе [Создание развертываний](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/hetzner-cloud-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/hetzner-cloud-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload") .

**Уничтожение ресурсов**

1. Из папки quickstart/rancher/hcloud выполнить terraform destroy --auto-approve.

Дождитесь подтверждения, что все ресурсы уничтожены.
