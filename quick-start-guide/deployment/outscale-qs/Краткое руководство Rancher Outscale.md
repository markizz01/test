


Прочтите это пошаговое руководство Rancher Outscale, чтобы быстро развернуть сервер Rancher с подключенным нижестоящим кластером Kubernetes с одной нодой.

Следующие шаги позволят быстро развернуть сервер Rancher на Outscale в single-node (одноузловом) кластере K3s Kubernetes с присоединенным single-node нисходящим кластером Kubernetes.

**Примечание.** Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Эти руководства не предназначены для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/outscale-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/outscale-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

**Необходимое условие**

**Внимание** . За развертывание на уровне Outscale взимается плата.

- [Учетная запись Outscale](https://en.outscale.com/ "https://en.outscale.com/") : вам потребуется учетная запись Outscale, так как именно здесь будут работать сервер и кластер.
- ([Ключ доступа) Outscale Access Key](https://docs.outscale.com/en/userguide/About-Access-Keys.html "https://docs.outscale.com/en/userguide/About-Access-Keys.html") : используйте эти инструкции для создания ключа доступа Outscale, если у вас его нет.
- [Terraform](https://www.terraform.io/downloads.html "https://www.terraform.io/downloads.html") : используется для предоставления сервера и кластера в Outscale.

**Начало работы**

1. Клонируйте [Rancher Quickstart](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") в папку с помощью git clone https://github.com/rancher/quickstart.
1. Перейдите в папку Outscale, содержащую файлы terraform, выполнив cd quickstart/rancher/outscale.
1. Переименуйте terraform.tfvars.example в terraform.tfvars.
1. Отредактируйте terraform.tfvarsи настройте следующие переменные:
- access\_key\_id- Ключ доступа 
- secret\_key\_id- ключ секрета
- rancher\_server\_admin\_password- Пароль администратора для созданного сервера Rancher
1. **Необязательно:** измените необязательные переменные в файлах terraform.tfvars. Для получения дополнительной информации см . ознакомительные сведения о быстром запуске и ознакомительные сведения о [быстром запуске ](https://github.com/rancher/quickstart/tree/master/rancher/outscale "https://github.com/rancher/quickstart/tree/master/rancher/outscale")[Outscale](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") . Предложения включают:
- region- Область за пределами масштаба, выберите ближайшую вместо значения по умолчанию ( eu-west-2)
- prefix- Префикс для всех созданных ресурсов
- instance\_type- Тип экземпляра, минимум требуется tinav3.c2r4p3
1. Переходим к  terraform init.
1. Чтобы инициировать создание среды, запустите terraform apply --auto-approve. Затем дождитесь вывода, подобного следующему:



Apply complete! Resources: 21 added, 0 changed, 0 destroyed.



Outputs:



rancher\_node\_ip = xx.xx.xx.xx

rancher\_server\_url = https://rancher.xx.xx.xx.xx.sslip.io

workload\_node\_ip = yy.yy.yy.yy



\8.  Вставьте rancher\_server\_ur lиз вывода выше в браузер. Войдите в систему, когда будет предложено (имя пользователя по умолчанию admin, используйте пароль, указанный в rancher\_server\_admin\_password).

\9. ssh к серверу Rancher, использует ключ id\_rsa, сгенерированный в quickstart/rancher/outscale.

**Результат**

В вашей учетной записи Outscale развернуты два кластера Kubernetes, один из которых работает с сервером Rancher, а другой готов к экспериментальному развертыванию. Обратите внимание, что, несмотря на то, что эта установка является отличным способом изучить функциональность Rancher, производственная установка должна соответствовать нашим рекомендациям по настройке высокой доступности. Ключи SSH для виртуальных машин генерируются автоматически и сохраняются в каталоге модуля.

**Что дальше?**

Используйте Rancher для создания развертывания. Дополнительные сведения см. в разделе [Создание развертываний](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/outscale-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/outscale-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload") .

**Уничтожение ресурсов**

1. Из папки quickstart/rancher/outscale выполнить terraform destroy --auto-approve.

Дождитесь подтверждения, что все ресурсы уничтожены.
