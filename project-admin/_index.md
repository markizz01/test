Проекты — это объекты, введенные в Rancher, которые помогают организовать пространства имен в вашем кластере Kubernetes. Вы можете использовать проекты для создания многопользовательских кластеров, что позволяет группе пользователей совместно использовать одни и те же базовые ресурсы без взаимодействия с приложениями друг друга.

С точки зрения иерархии:
-	Кластеры содержат проекты
-	Проекты содержат пространства имен

В Rancher проекты позволяют управлять несколькими пространствами имен как единым целым. В базовом Kubernetes, который не включает проекты, такие функции, как права доступа на основе ролей или ресурсы кластера, назначаются отдельным пространствам имен. В кластерах, где для нескольких пространств имен требуется один и тот же набор прав доступа, назначение этих прав каждому отдельному пространству имен может стать утомительным. Несмотря на то, что для всех пространств имен требуются одинаковые права, невозможно применить эти права ко всем вашим пространствам имен за одно действие. Вам пришлось бы повторно назначать эти права каждому пространству имен!

Проекты Rancher решают эту проблему, позволяя применять ресурсы и права доступа на уровне проекта. Затем каждое пространство имен в проекте наследует эти ресурсы и политики, поэтому вам нужно назначить их проекту только один раз, а не каждому отдельному пространству имен.

Вы можете использовать проекты для выполнения таких действий, как:
-	[Назначение пользователям доступа к группе пространств имен](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/project-members)
-	[Назначение пользователям определенных ролей в проекте .  Роль владельца, участника, «только для чтения» или пользователя .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/rbac/default-custom-roles)
-	[Установка квоты ресурсов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/resource-quotas)
-	[Управление пространствами имен](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/namespaces)
-	[Настройка инструментов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/tools)
-	[Настройка конвейеров для непрерывной интеграции и развертывания](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/pipelines)
-	[Настройка политик безопасности модуля](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/project-admin/pod-security-policies)

# Авторизация
Пользователи без прав администратора получают доступ к проекту только после того, как [администратор](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/rbac/global-permissions) , [владелец кластера или участник или владелец проекта](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/rbac/cluster-project-roles/#cluster-roles) [добавит](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/rbac/cluster-project-roles/#project-roles) их во вкладку " Участники " проекта .
Тот, кто создает проект, автоматически становится его [владельцем .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/project-admin/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/admin-settings/rbac/cluster-project-roles/#project-roles)

# Переключение между проектами

Для переключения между проектами используйте раскрывающийся список на панели навигации. Кроме того, вы можете переключаться между проектами прямо на панели навигации.
1.	В левом верхнем углу нажмите **☰ > Управление кластером .**
2.	На странице **Кластеры** перейдите к кластеру, в котором вы хотите переключить проекты, и нажмите **Исследовать .**
3.	В верхней панели навигации выберите проект, который хотите открыть.

