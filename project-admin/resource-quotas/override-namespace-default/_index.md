Хотя **предел пространства имен по умолчанию** распространяется от проекта к каждому пространству имен при создании, в некоторых случаях может потребоваться увеличить (или уменьшить) квоты для определенного пространства имен. В этой ситуации вы можете переопределить/отменить ограничения по умолчанию, отредактировав пространство имен.

На приведенной ниже диаграмме администратор Rancher имеет действующую квоту ресурсов для своего проекта. Однако администратор хочет переопределить ограничения пространства имен Namespace 3,  чтобы иметь больше доступных ресурсов. Поэтому администратор увеличивает ограничения пространства имен Namespace 3, чтобы пространство имен могло получить доступ к большему количеству ресурсов.
[Переопределение ограничения пространства имен по умолчанию](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/resource-quotas/override-namespace-default/%7B%7B%3Cbaseurl%3E%7D%7D/img/rancher/rancher-resource-quota-override.svg)    

Практическое руководство. [Редактирование квот ресурсов пространства имен](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/resource-quotas/override-namespace-default/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/cluster-admin/projects-and-namespaces)

# Редактирование квот ресурсов пространства имен

Если для проекта настроена квота ресурсов, вы можете переопределить ограничение пространства имен по умолчанию, чтобы предоставить определенному пространству имен доступ к большему (или меньшему) количеству ресурсов проекта.
1.	В левом верхнем углу нажмите **☰ > Cluster Management  Управление кластером .**
2.	На странице **« Кластеры »** перейдите к кластеру, в котором вы хотите изменить квоту ресурса пространства имен, и нажмите **«Explore  Исследовать » .**
3.	Щелкните **Cluster > Projects/Namespaces Кластер > Проекты/пространства имен .**
4.	Найдите пространство имен, для которого вы хотите изменить квоту ресурсов. Нажмите **⋮ > Edit Config Изменить конфигурацию .**
5.	Отредактируйте лимиты ресурсов. Эти ограничения определяют ресурсы, доступные пространству имен. Ограничения должны быть установлены в пределах настроенных ограничений проекта.

Дополнительные сведения о каждом **типе ресурсов** [см. в справочнике по типам .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/resource-quotas/override-namespace-default/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/resource-quotas/quota-type-reference)

***Примечание:***
-	Если для проекта не настроена квота ресурсов, эти параметры будут недоступны.
-	Если вы введете ограничения, которые превышают настроенные ограничения проекта, Rancher не позволит вам сохранить ваши изменения.

**Результат:** ваше переопределение применено к квоте ресурсов пространства имен.
