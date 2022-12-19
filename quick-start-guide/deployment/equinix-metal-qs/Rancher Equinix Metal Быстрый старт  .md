


### **Эта инструкция покажет следующее:**

- Инициализация сервера Equinix Metal
- Установка Rancher 2.x
- Создание вашего первого кластера
- Развертывание приложения, Nginx

### Примечание.
Целью этих руководств является быстрый запуск песочницы, которую вы можете использовать для оценки Rancher. Установка Docker не рекомендуется для производственных сред. Подробные инструкции по установке см . в разделе [Установка](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation") .

### **Схема быстрого старта**

Это краткое руководство разделено на различные задачи для более удобного использования.

1. [Предоставление хоста Equinix Metal](https://github.com/markizz01/test/blob/main/quick-start-guide/deployment/equinix-metal-qs/Rancher%20Equinix%20Metal%20Быстрый%20старт%20%20.md#предоставление-хостаequinixmetal)
2. [Установить Rancher ](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/_index.md#2-install-rancher")
3. [Авторизоваться](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/_index.md#3-log-in")
4. [Создайте кластер](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/_index.md#4-create-the-cluster")

### **Начало работы**

- Аккаунт Equinix Metal
- Проект [Equinix Metal](https://metal.equinix.com/developers/docs/accounts/projects/ "https://metal.equinix.com/developers/docs/accounts/projects/")

##  Предоставление хоста Equinix Metal**

Начните развертывание Equinix Metal Host. Серверы Equinix Metal можно настроить с помощью консоли Equinix Metal, api или cli. Вы можете найти инструкции по развертыванию с каждым типом [развертывания в документации по развертыванию Equinix Metal](https://metal.equinix.com/developers/docs/deploy/on-demand/ "https://metal.equinix.com/developers/docs/deploy/on-demand/") . Yopu может найти дополнительную документацию по типам и ценам серверов Equinix Metal ниже.

- [Типы металлических серверов Equinix](https://metal.equinix.com/developers/docs/servers/about/ "https://metal.equinix.com/developers/docs/servers/about/")
- [ Equinix Metal оценка](https://metal.equinix.com/developers/docs/servers/server-specs/ "https://metal.equinix.com/developers/docs/servers/server-specs/")



### ***Примечание:***

При подготовке нового Equinix Metal Server через интерфейс командной строки или API вам потребуется предоставить следующую информацию: идентификатор проекта, план, metro и операционную систему. При использовании виртуальной машины, размещенной в облаке, вам необходимо разрешить входящие TCP комуникаторы с портами 80 и 443. Информацию о настройке портов см. в документации вашего облачного хоста. Полный список требований к порту см. в [разделе Установка Docker](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning/node-requirements "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-provisioning/node-requirements") . Подготовьте хост в соответствии с нашими [Требованиями](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/requirements "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/deployment/equinix-metal-qs/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/installation/requirements") .

## Установите Rancher**

Чтобы установить Rancher на свой хост Equinix Metal, подключитесь к нему, а затем используйте shell (командную строку) для установки.

1. Войдите на свой хост Equinix Metal, используя предпочтительный shell, например PuTTy, или подключение к удаленному терминалу.
2. В вашей shell введите следующую команду:
3. 
```
sudo docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged rancher/rancher
```
\*\*Result:\*\* Rancher is installed.



\### 3. Log In



Log in to Rancher to begin using the application. After you log in, you'll make some one-time configurations.



\1.  Open a web browser and enter the IP address of your host: `https://<SERVER\_IP>`.



`  `Replace `<SERVER\_IP>` with your host IP address.



\2.  When prompted, create a password for the default `admin` account there cowpoke!



\3. Set the \*\*Rancher Server URL\*\*. The URL can either be an IP address or a host name. However, each node added to your cluster must be able to connect to this URL.<br/><br/>If you use a hostname in the URL, this hostname must be resolvable by DNS on the nodes you want to add to you cluster.



<br/>



\### 4. Create the Cluster



Welcome to Rancher! You are now able to create your first Kubernetes cluster.



In this task, you can use the versatile \*\*Custom\*\* option. This option lets you add \_any\_ Linux host (cloud-hosted VM, on-prem VM, or bare-metal) to be used in a cluster.



\1.  Click \*\*☰ > Cluster Management\*\*.

\1. From the \*\*Clusters\*\* page, click \*\*Create\*\*.

\2. Choose \*\*Custom\*\*.



\3. Enter a \*\*Cluster Name\*\*.



\4. Skip \*\*Member Roles\*\* and \*\*Cluster Options\*\*. We'll tell you about them later.



\5. Click \*\*Next\*\*.



\6. From \*\*Node Role\*\*, select \_all\_ the roles: \*\*etcd\*\*, \*\*Control\*\*, and \*\*Worker\*\*.



\7. \*\*Optional\*\*: Rancher auto-detects the IP addresses used for Rancher communication and cluster communication. You can override these using `Public Address` and `Internal Address` in the \*\*Node Address\*\* section.



\8. Skip the \*\*Labels\*\* stuff. It's not important for now.



\9. Copy the command displayed on screen to your clipboard.



\10. Log in to your Linux host using your preferred shell, such as PuTTy or a remote Terminal connection. Run the command copied to your clipboard.



\11. When you finish running the command on your Linux host, click \*\*Done\*\*.



\*\*Result:\*\*



Your cluster is created and assigned a state of \*\*Provisioning\*\*. Rancher is standing up your cluster.



You can access your cluster after its state is updated to \*\*Active\*\*.



\*\*Active\*\* clusters are assigned two Projects:



\- `Default`, containing the `default` namespace

\- `System`, containing the `cattle-system`, `ingress-nginx`, `kube-public`, and `kube-system` namespaces



\#### Finished



Congratulations! You have created your first cluster.



\#### What's Next?



Use Rancher to create a deployment. For more information, see [Creating Deployments]({{<baseurl>}}/rancher/v2.6/en/quick-start-guide/workload).

