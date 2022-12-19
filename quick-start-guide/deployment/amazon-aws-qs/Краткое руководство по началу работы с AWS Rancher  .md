


Прочтите это пошаговое руководство Rancher AWS, чтобы быстро развернуть сервер Rancher с подключенным нижестоящим кластером Kubernetes с одним узлом.

Следующие шаги позволят быстро развернуть сервер Rancher на AWS в кластере K3s Kubernetes single-node (с одним узлом), к которому подключен нижестоящий кластер Kubernetes single-node.

**Примечание.** Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Эти руководства не предназначены для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

**Необходимые условия**

***Внимание*** . За развертывание в Amazon AWS взимается плата.

- [Учетная запись](https://aws.amazon.com/account/ "https://aws.amazon.com/account/") Amazon AWS. Учетная запись Amazon AWS требуется для создания ресурсов для развертывания Rancher и Kubernetes.
- [Ключ доступа к Amazon AWS](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html "https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html") . Воспользуйтесь этой ссылкой, чтобы следовать руководству по созданию ключа доступа к Amazon AWS, если у вас его еще нет.
- [Созданная IAM-политика](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html "https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-start") : определяет разрешения, которые имеет учетная запись, связанная с этой политикой.
- Установка Terraform : используется для предоставления сервера и кластера в Amazon AWS.

**Пример IAM-политики**

Модуль AWS просто создает пару ключей EC2, группу безопасности EC2 и экземпляр EC2. Простая политика будет:
``` 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*"
        }
    ]
}
```

**Начало работы**

1. Клонируйте [Rancher Quickstart](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") в папку с помощью git clone https://github.com/rancher/quickstart.
2. Перейдите в папку AWS, содержащую файлы terraform, выполнив cd quickstart/rancher/aws.
3. Переименуйте terraform.tfvars.example  в terraform.tfvars.
4. Отредактируйте terraform.tfvars и настройте следующие переменные:
- aws\_access\_key- Ключ доступа Amazon AWS
- aws\_secret\_key- Секретный ключ Amazon AWS
- rancher\_server\_admin\_password- Пароль администратора для созданного сервера Rancher
5. **Необязательно/опционно:** измените необязательные переменные в файлах terraform.tfvars. Дополнительную информацию см. в справочных материалах по [быстрому запуску](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") и в справочных материалах по [быстрому запуску AWS](https://github.com/rancher/quickstart/tree/master/rancher/aws "https://github.com/rancher/quickstart/tree/master/rancher/aws") . Предложения включают:
- aws\_region- Регион Amazon AWS, выберите ближайший вместо стандартного ( us-east-1)
- prefix- Префикс для всех созданных ресурсов
- instance\_type- Используемый размер инстанса EC2, минимальный, t3a.medium, но может быть использован t3a.large или  t3a.xlarge, если они находятся в рамках бюджета
- add\_windows\_node- Если true, в кластер рабочей нагрузки добавляется дополнительный рабочий узел Windows.
6. Переходим к terraform init.
7. Чтобы инициировать создание среды, запустите terraform apply --auto-approve. Затем дождитесь вывода, подобного следующему:


```
Apply complete! Resources: 16 added, 0 changed, 0 destroyed.


Outputs:

rancher\_node\_ip = xx.xx.xx.xx

rancher\_server\_url = https://rancher.xx.xx.xx.xx.sslip.io

workload\_node\_ip = yy.yy.yy.yy
```
8. Вставьте rancher\_server\_url из вывода выше в браузер. Войдите в систему, когда будет предложено (имя пользователя по умолчанию admin, используйте пароль, указанный в rancher\_server\_admin\_password).
9. SSH для сервера Rancher, использует id\_rsa - ключ сгенерированный в quickstart/rancher/aws.

**Результат**

В вашей учетной записи AWS развернуты два кластера Kubernetes, один из которых работает с Rancher Server, а другой готов к экспериментальному развертыванию. Обратите внимание, что, несмотря на то, что эта установка является отличным способом изучить функциональность Rancher, производственная установка должна соответствовать нашим рекомендациям по настройке высокой доступности. Ключи SSH для виртуальных машин генерируются автоматически и сохраняются в каталоге модуля.

**Что дальше?**

Используйте Rancher для создания развертывания. Дополнительные сведения см. в разделе [Создание развертываний](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload") . <https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload> 

**Ликвидация ресурса**

1. Из папки quickstart/rancher/aws выполнить terraform destroy --auto-approve.

2. Дождитесь подтверждения, что все ресурсы уничтожены.
