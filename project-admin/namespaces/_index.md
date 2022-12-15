# Пространства имен (Namespaces)

В Rancher вы можете дополнительно разделить проекты на разные пространства имен , которые представляют собой виртуальные кластеры внутри проекта, поддерживаемые физическим кластером. Если вам требуется другой уровень организации помимо проектов и пространства имен default, вы можете использовать несколько пространств имен для изоляции приложений и ресурсов.

Хотя вы назначаете ресурсы на уровне проекта, чтобы каждое пространство имен в проекте могло их использовать, вы можете переопределить это наследование, явно назначив ресурсы пространству имен.

Ресурсы, которые вы можете назначать непосредственно пространствам имен, включают:
-	[Нагрузки (Workloads)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/workloads)
-	[Балансировщики нагрузки/вход(Load Balancers/Ingress)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/load-balancers-and-ingress)
-	[Записи обнаружения службы(Service Discovery Records)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/service-discovery)
-	[Постоянные заявки на объем (Persistent Volume Claims)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-admin/volumes-and-storage)
-	[Сертификаты (Certificates)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/certificates)
-	[Карты конфигурации (ConfigMaps)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/configmaps)
-	[Реестры (Registries)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/registries)
-	[Секреты (Secrets)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/secrets)

Чтобы управлять разрешениями в обычном кластере Kubernetes, администраторы кластера настраивают политики доступа на основе ролей для каждого пространства имен. Вместо этого в Rancher разрешения пользователей назначаются на уровне проекта, и разрешения автоматически наследуются любым пространством имен, принадлежащим конкретному проекту.

***Примечание.** Если вы создаете пространство имен с помощью kubectl, оно может оказаться непригодным для использования, поскольку kubectl не требует, чтобы ваше новое пространство имен было ограничено проектом, к которому у вас есть доступ. Если ваши разрешения ограничены уровнем проекта, [лучше создать пространство имен через Rancher](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/namespaces) , чтобы гарантировать, что у вас будет разрешение на доступ к пространству имен.*

# Создание пространств имен

Создайте новое пространство имен, чтобы изолировать приложения и ресурсы в проекте.
**Совет.** При работе с ресурсами проекта, которые можно назначить пространству имен (например, рабочим [нагрузкам](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/workloads/deploy-workloads) , [сертификатам](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/certificates) , [картам конфигурации](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/configmaps) и т. д .), пространство имен можно создать на ходу.

1.	В левом верхнем углу нажмите **☰ > Cluster Management Управление кластером .**
2.	На странице **Clusters Кластеры** перейдите к кластеру, в котором вы хотите создать пространство имен, и нажмите **Explore Исследовать .**
3.	Щелкните **Cluster > Projects/Namespaces Кластер > Проекты/пространства имен .**
4.	Перейдите к проекту, в который вы хотите добавить пространство имен, и нажмите **«Create Namespace Создать пространство имен »** . В качестве альтернативы перейдите к разделу **«Not in a Project Не в проекте» **, чтобы создать пространство имен, не связанное с проектом.
5.	*Необязательно: если в вашем проекте действуют [квоты ресурсов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/resource-quotas) , вы можете переопределить Limits лимиты ресурсов по умолчанию (которые ограничивают ресурсы, которые может потреблять пространство имен).*
6.	Введите **Name  имя** и нажмите **« Create Создать »** .

**Результат:** ваше пространство имен добавлено в проект. Вы можете начать назначать ресурсы кластера пространству имен.

# Перенос пространств имен в другой проект

Администраторам и участникам кластера может иногда потребоваться переместить пространство имен в другой проект, например, когда вы хотите, чтобы другая команда начала использовать приложение.
1.	В левом верхнем углу нажмите ☰ > Управление кластером .
2.	На странице Кластеры перейдите к кластеру, в который вы хотите переместить пространство имен, и щелкните Исследовать .
3.	Щелкните Кластер > Проекты/пространства имен .
4.	Перейдите к пространству имен, которое вы хотите переместить, и нажмите ⋮ > Move Переместить .
5.	Выберите пространство имен, которое вы хотите переместить в другой проект. Затем нажмите Move Переместить . Вы можете перемещать несколько пространств имен одновременно.
***Замечания:**
-	Не перемещайте пространства имен в проекте System. Перемещение этих пространств имен может отрицательно сказаться на работе кластерной сети.
-	Вы не можете переместить пространство имен в проект, для которого уже настроена [квота ресурсов .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/resource-quotas)
-	Если вы перемещаете пространство имен из проекта с установленной квотой в проект без установленной квоты, квота удаляется из пространства имен.
6.  Выберите новый проект для нового пространства имен и нажмите «Move Переместить» . Кроме того, вы можете удалить пространство имен из всех проектов, выбрав None .
Результат: Ваше пространство имен перемещено в другой проект (или отсоединено от всех проектов). Если какие-либо ресурсы проекта присоединены к пространству имен, пространство имен освобождает их, а затем присоединенные ресурсы из нового проекта.*

# Редактирование квот ресурсов пространства имен

Вы всегда можете переопределить ограничение пространства имен по умолчанию, чтобы предоставить определенному пространству имен доступ к большему (или меньшему) количеству ресурсов проекта.

Дополнительные сведения см. в разделе, как изменить [квоты ресурсов пространства имен](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/namespaces/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/resource-quotas/override-namespace-default)
