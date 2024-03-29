﻿


### На этой странице объясняются концепции, связанные с Kubernetes, которые важны для понимания того, как работает Rancher. В приведенных ниже описаниях представлен упрощенный обзор компонентов Kubernetes. Дополнительные сведения см. в [официальной документации по компонентам Kubernetes.](https://kubernetes.io/docs/concepts/overview/components/ "https://kubernetes.io/docs/concepts/overview/components/")

## **Docker**

Docker — это стандарт упаковки контейнеров и стандарт времени выполнения. Разработчики создают образы контейнеров из Dockerfiles и распространяют образы контейнеров из реестров Docker. [Docker Hub](https://hub.docker.com/ "https://hub.docker.com/") — самый популярный публичный реестр. Многие организации также создают частные реестры Docker. Docker в основном используется для управления контейнерами на отдельных узлах.

***Примечание*.** Хотя Rancher 1.6 поддерживал технологию кластеризации Docker Swarm, она больше не поддерживается в Rancher 2.x из-за успеха Kubernetes.

## **Kubernetes.**

Kubernetes — это стандарт управления кластером контейнеров. Файлы YAML определяют контейнеры и другие ресурсы, формирующие приложение. Kubernetes выполняет такие функции, как планирование, масштабирование, обнаружение сервисов, проверка работоспособности, управление секретами и управление конфигурацией.

## **Что такое кластер Kubernetes?**

Кластер — это группа компьютеров, которые работают вместе как единая система.

Кластер *Kubernetes* — это кластер, использующий систему [оркестрации контейнеров Kubernetes](https://kubernetes.io/ "https://kubernetes.io/") для развертывания, обслуживания и масштабирования контейнеров Docker, что позволяет вашей организации автоматизировать операции приложений.

## **Роли для узлов в кластерах Kubernetes**

Каждый вычислительный ресурс в кластере Kubernetes называется *нодом* . Ноды могут быть как «голыми» серверами, так и виртуальными машинами. Kubernetes классифицирует ноды по трем типам: ноды *etcd* , ноды уровня *управления* и *рабочие* ноды.

Кластер Kubernetes состоит как минимум из одного etcd, controlplane и рабочего нода.

## **Ноды etcd**

Rancher использует etcd в качестве хранилища данных как в установках с одним нодом, так и в установках с высокой доступностью. В Kubernetes etcd также является ролью для нодов, которые хранят состояние кластера.

Состояние кластера Kubernetes сохраняется в [etcd. ](https://kubernetes.io/docs/concepts/overview/components/ "https://kubernetes.io/docs/concepts/overview/components/#etcd")Узлы etcd запускают базу данных etcd.

Компонент базы данных etcd — это распределенное хранилище ключей и значений, используемое в качестве хранилища Kubernetes для всех данных кластера, таких как координирование кластера и управление состоянием. Рекомендуется запускать etcd на нескольких нодах, чтобы всегда была доступна резервная копия для отработки отказа.

Хотя вы можете запустить etcd только на одном ноде, для согласования обновлений состояния кластера etcd требуется большинство нодов т. е. кворум. Кластер всегда должен содержать достаточно работоспособных нодовetcd для формирования кворума. Для кластера с n участниками кворум равен (n/2)+1. Для любого кластера нечетного размера добавление одного нода всегда увеличивает количество нодов, необходимых для кворума.

Трех нодов etcd обычно достаточно для небольших кластеров и пяти нодов etcd для больших кластеров.

## **Ноды Controlplane (плоскости управления)**

Ноды Controlplane запускают сервер Kubernetes API, планировщик и диспетчер контроллеров. Эти нодывыполняют рутинные задачи, гарантируя, что ваш кластер поддерживает вашу конфигурацию. Поскольку все данные кластера хранятся на ваших гнодах etcd, ноды Controlplane не имеют состояния. Вы можете запустить Controlplane на одном ноде, хотя для резервирования рекомендуется использовать три или более нода. Кроме того, один нод может совместно использовать роли Controlplane и etcd.

## **Рабочие ноды**

Каждый [рабочий нод](https://kubernetes.io/docs/concepts/architecture/nodes/ "https://kubernetes.io/docs/concepts/architecture/nodes/") выполняет следующее:

- **Kubelets:** агент, который отслеживает состояние нода, обеспечивая работоспособность ваших контейнеров.
- **Рабочие нагрузки:** контейнеры и модули, содержащие ваши приложения, а также другие типы развертываний.

Рабочие ноды также запускают драйверы хранилища и сети, а также контроллеры входящего трафика, когда это необходимо. Вы создаете столько рабочих нодов, сколько необходимо для выполнения ваших [рабочих нагрузок](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/concepts/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/workloads "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/overview/concepts/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/workloads") .

## **Helm**

  Для высокодоступных установок Rancher, Helm — это инструмент, используемый для установки Rancher в кластере Kubernetes.

Helm — это предпочтительный инструмент управления пакетами для Kubernetes. Чарты Helm предоставляют синтаксис шаблонов для документов декларации Kubernetes YAML. С помощью Helm мы можем создавать настраиваемые развертывания, а не просто использовать статические файлы. Дополнительные сведения о создании собственного каталога развертываний см. в документации по адресу <https://helm.sh/> .

Дополнительные сведения об учетных записях служб и привязке ролей кластера см. в [документации Kubernetes.](https://kubernetes.io/docs/reference/access-authn-authz/rbac/ "https://kubernetes.io/docs/reference/access-authn-authz/rbac/")

