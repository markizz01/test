Для обеспечения согласованности и соответствия требованиям каждой структуре необходима возможность автоматически определять и применять политики в своем окружении. [OPA (Open Policy Agent)](https://www.openpolicyagent.org/) — это механизм политик, который упрощает управление на основе политик для собственных облачных сред. Rancher предоставляет возможность включить OPA Gatekeeper в кластерах Kubernetes, а также устанавливает пару встроенных определений политик, которые также называются шаблонами ограничений.
OPA предоставляет декларативный язык высокого уровня, который позволяет указать политику в виде кода и возможность расширения простых API-интерфейсов, чтобы разгрузить принятие решений о политике.

[OPA Gatekeeper](https://www.openpolicyagent.org/) — это проект, обеспечивающий интеграцию между OPA и Kubernetes. OPA Gatekeeper обеспечивает:

-	Расширяемую параметризованную политику библиотек.
-	Собственные CRD Kubernetes для создания экземпляра политики библиотеки, называемые «ограничениями».
-	Собственные CRD Kubernetes для расширения политики библиотеки, называемые «шаблонами ограничений».
-	Функционал аудита.

Чтобы узнать больше об OPA, обратитесь к [официальной документации.](https://www.openpolicyagent.org/docs/latest/)

# Как работает интеграция OPA Gatekeeper 

Kubernetes предоставляет возможность расширять функциональные возможности сервера API с помощью веб-перехватчиков webhooks (контроллера допуска), которые вызываются всякий раз, когда ресурс создается, обновляется или удаляется. Gatekeeper устанавливается как проверяющий веб-перехватчик и применяет политики, определенные определениями пользовательских ресурсов Kubernetes. В дополнение к использованию контроля доступа Gatekeeper предоставляет возможность аудита существующих ресурсов в кластерах Kubernetes и отметки текущих нарушений включенных политик.
OPA Gatekeeper доступен через системную Rancher's Helm и установлен в пространстве имен с именем gatekeeper-system.



# Включение OPA Gatekeeper в кластере
В Rancher v2.5 улучшено приложение OPA Gatekeeper. Функция Rancher v2.4 не может быть обновлена до новой версии в Rancher v2.5. Если вы установили OPA Gatekeeper в Rancher v2.4, вам потребуется удалить OPA Gatekeeper и его CRD из старого пользовательского интерфейса, а затем переустановить его в Rancher v2.5. Чтобы удалить CRD, выполните следующую команду в консоли kubectl  kubectl delete crd configs.config.gatekeeper.sh constrainttemplates.templates.gatekeeper.sh.

**Предварительное условие:** только администраторы и владельцы кластера могут включить OPA Gatekeeper

Диаграмму OPA Gatekeeper Helm можно установить из **Apps & Marketplace .**

# Включение привратника OPA
1.	В левом верхнем углу нажмите **☰ > Cluster Management. (Управление кластером) .**
2.	На странице **Clusters** перейдите к кластеру, в котором вы хотите включить OPA Gatekeeper, и щелкните **Explore .**
3.	На левой панели навигации щелкните **Apps & Marketplace .**
4.	Щелкните **Charts** и щелкните **OPA Gatekeeper.**
5.	Щелкните **Install (Установить) .**
**Результат:** OPA Gatekeeper развернут в вашем кластере Kubernetes.

# Шаблоны ограничений

[Шаблоны ограничений](https://github.com/open-policy-agent/gatekeeper#constraint-templates) — это настраиваемые ресурсы Kubernetes, которые определяют схему и логику Rego политики OPA, применяемой Gatekeeper. Дополнительные сведения о языке политики Rego [см. в официальной документации.](https://www.openpolicyagent.org/docs/latest/policy-language/)

Когда OPA Gatekeeper включен, Rancher по умолчанию устанавливает некоторые шаблоны.

Чтобы просмотреть список шаблонов ограничений, установленных в кластере, перейдите в левое боковое меню в разделе OPA Gatekeeper и щелкните **Templates .**

Rancher также предоставляет возможность создавать собственные шаблоны ограничений, импортируя определения YAML.

# Создание и настройка ограничений

[Ограничения](https://github.com/open-policy-agent/gatekeeper#constraints) — это настраиваемые ресурсы Kubernetes, определяющие область объектов, к которым применяется определенный шаблон ограничения. Полная политика определяется шаблонами ограничений и ограничениями вместе.

**Предварительные требования:** в кластере должен быть включен OPA Gatekeeper.

Чтобы просмотреть установленные ограничения, перейдите в левое боковое меню в разделе OPA Gatekeeper и нажмите **« Constraints (Ограничения) » .**

Новые ограничения могут быть созданы из шаблона ограничений.

Rancher предоставляет возможность создать ограничение с помощью удобной формы, позволяющей вводить различные поля ограничений.

Параметр **« Edit as yaml (Редактировать как yaml) »** также доступен для настройки определения ограничения yaml.

## Освобождение системных пространств имен Rancher от ограничений

При создании ограничения убедитесь, что оно не применяется ни к каким системным namespaces (пространствам имен) Rancher или Kubernetes. Если системные пространства имен не исключены, то можно увидеть много ресурсов под ними, помеченных как нарушения ограничения.

Чтобы ограничить область действия ограничения только пространствами имен пользователей, всегда указывайте эти пространства имен в поле **Match** ограничения.

Кроме того, ограничение может мешать другим функциям Rancher и препятствовать развертыванию системных рабочих нагрузок. Чтобы избежать этого, исключите все пространства имен, специфичные для Rancher, из ваших ограничений.

# Применение ограничений в вашем кластере

Если в качестве **принудительного действия** установлено значение **« Deny (отклонить)»**, ограничение немедленно включается и будет отклонять любые запросы, нарушающие заданную политику. По умолчанию значением принудительного применения является **Deny.**

Если **принудительное действие — Dryrun (пробный запуск)**, любые ресурсы, нарушающие политику, записываются только в поле состояния ограничения.

Чтобы применить ограничения, создайте ограничение с помощью формы. В поле **« Enforcement Action (принудительные меры)»** выберите **«Deny».**

# Аудит и нарушения в вашем кластере

OPA Gatekeeper выполняет периодический аудит, чтобы проверить, не нарушает ли какой-либо существующий ресурс какое-либо принудительное ограничение. Интервал аудита (по умолчанию 300 с) можно настроить при установке Gatekeeper.

На странице Gatekeeper перечислены все нарушения определенных ограничений.

Также в разделе **« Constraints (Ограничения)»** можно найти количество нарушений ограничений.

Подробное представление каждого ограничения содержит информацию о ресурсе, нарушившем ограничение.

## Отключение OPA Gatekeeper .

1.	Перейдите к представлению  Dashboard кластера.
2.	В левом боковом меню разверните меню кластера и нажмите **OPA Gatekeeper .**
3.	Нажмите **⋮> Disable (Отключить).**

**Результат:** При отключении OPA Gatekeeper все шаблоны ограничений и сами ограничения также будут удалены.
