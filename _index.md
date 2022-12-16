|Что такое Rancher|
|:-|:-|:-|:-|:-|:-|:-|
|заглавие	|короткое название	|описание	|метазаголовок	|метаописание	|вставкаOneSix	|псевдонимы|
|:-|:-|:-|:-|:-|:-|:-|
|Ранчер 2.6	|Ранчер 2.6 (последняя версия)	|Rancher значительно повышает ценность Kubernetes: управление сотнями кластеров из одного интерфейса, централизация RBAC, возможность мониторинга и оповещения.| 	Документы Rancher 2.6: что нового?	|Rancher 2 значительно расширяет возможности Kubernetes: управление сотнями кластеров из одного интерфейса, централизация RBAC, возможность мониторинга и оповещения. |	ЛОЖЬ	|/ранчер/v2.x/ru/|


Первоначально Rancher был создан для работы с несколькими оркестраторами (наборами инструментов), и в нем был собственный оркестратор под названием Cattle. С появлением Kubernetes на рынке, Rancher 2 эксклюзивно развертывает и управляет кластерами Kubernetes, работающими где угодно и у любого провайдера.

Rancher может установить Kubernetes от организованного провайдера, выделить вычислительные узлы, а затем установить на них Kubernetes или импортировать существующие кластеры Kubernetes, работающие где угодно.

Rancher значительно повышает ценность Kubernetes, во-первых, путем централизации аутентификации и управления доступом на основе ролей (RBAC) для всех кластеров, что дает глобальным администраторам возможность контролировать доступ к кластеру из одного места.

Затем он обеспечивает подробный мониторинг и оповещение о кластерах и их ресурсах, отправляет журналы внешним поставщикам и напрямую интегрируется с Helm через каталог приложений. Если у вас есть внешняя система CI/CD, вы можете подключить ее к Rancher, но если у вас ее нет, то  Rancher включает в себя Fleet, чтобы помочь вам автоматически развертывать и обновлять рабочие нагрузки.

Rancher — это полноценная платформа управления контейнерами для Kubernetes, предоставляющая инструменты для успешного запуска Kubernetes где угодно.

