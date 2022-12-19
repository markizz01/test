

Прочтите это пошаговое руководство Rancher DigitalOcean, чтобы быстро развернуть сервер Rancher с подключенным нижестоящим кластером Kubernetes с одной нодой.

Следующие шаги позволят быстро развернуть сервер Rancher в DigitalOcean в single-node (одноузловом) кластере K3s Kubernetes с присоединенным одноузловым нисходящим кластером Kubernetes.

### Примечание.
Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Эти руководства не предназначены для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

### **Необходимые условия**

### ***Внимание*** . За развертывание в DigitalOcean взимается плата.

- [Учетная запись DigitalOcean](https://www.digitalocean.com/ "https://www.digitalocean.com/") : вам потребуется учетная запись в DigitalOcean, так как именно здесь будут работать сервер и кластер.
- [Ключ доступа к DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-create-a-digitalocean-space-and-api-key "https://www.digitalocean.com/community/tutorials/how-to-create-a-digitalocean-space-and-api-key") : используйте эту ссылку, чтобы создать ключ доступа к DigitalOcean, если у вас его нет.
- [Terraform](https://www.terraform.io/downloads.html "https://www.terraform.io/downloads.html") : используется для предоставления сервера и кластера DigitalOcean.

### **Начало работы**

1. Клонируйте [Rancher Quickstart](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") в папку с помощью git clone https://github.com/rancher/quickstart.
2. Перейдите в папку DigitalOcean, содержащую файлы terraform, выполнив cd quickstart/rancher/do.
3. Переименуйте terraform.tfvars.example в terraform.tfvars.
4. Отредактируйте terraform.tfvars и настройте следующие переменные:
- do\_token- Ключ доступа к DigitalOcean
- rancher\_server\_admin\_password- Пароль администратора для созданного сервера Rancher
5. **Необязательно:** измените необязательные переменные в файлах terraform.tfvars. Дополнительную информацию см. в файлах сведений о [быстром запуске](https://github.com/rancher/quickstart "https://github.com/rancher/quickstart") и в файле сведений о быстром запуске [DO](https://github.com/rancher/quickstart/tree/master/rancher/do "https://github.com/rancher/quickstart/tree/master/rancher/do") . Предложения включают:
- do\_region- Регион DigitalOcean, выберите ближайший вместо стандартного ( nyc1)
- prefix- Префикс для всех созданных ресурсов
- droplet\_size- используется Дроплет минимальный( s-2vcpu-4gbно) но может быть использован s-4vcpu-8gb, если позволяет бюджет
6. Переходим к terraform init.
7. Чтобы инициировать создание среды, запустите terraform apply --auto-approve. Затем дождитесь вывода, подобного следующему:

```

Apply complete! Resources: 15 added, 0 changed, 0 destroyed.



Outputs:



rancher\_node\_ip = xx.xx.xx.xx

rancher\_server\_url = https://rancher.xx.xx.xx.xx.sslip.io

workload\_node\_ip = yy.yy.yy.yy
```
8. Вставьте rancher\_server\_url из вывода выше в браузер. Войдите в систему, когда будет предложено (имя пользователя по умолчанию admin, используйте пароль, указанный в rancher\_server\_admin\_password).
9. SSH к серверу Rancher, использует ключ id\_rsa, сгенерированный в quickstart/rancher/do.

### **Результат**

Два кластера Kubernetes развернуты в вашей учетной записи DigitalOcean, один работает под управлением Rancher Server, а другой готов к экспериментальному развертыванию. Обратите внимание, что, несмотря на то, что эта установка является отличным способом изучить функциональность Rancher, производственная установка должна соответствовать нашим рекомендациям по настройке высокой доступности. Ключи SSH для виртуальных машин генерируются автоматически и сохраняются в каталоге модуля.

### **Что дальше?**

Используйте Rancher для создания развертывания. Дополнительные сведения см. в разделе [Создание развертываний](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/workload") .

### **Удалениие ресурсов**

1. Из quickstart/rancher/do выполнить terraform destroy --auto-approve.
2. Дождитесь подтверждения, что все ресурсы уничтожены.

