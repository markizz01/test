Этот раздел относится к узлам с ролью controlplane.

**Проверьте, запущены ли контейнеры Controlplane**

На узлах с controlplane запущено три конкретных контейнера:
-	kube-apiserver
-	kube-controller-manager
-	kube-scheduler

Контейнеры должны иметь статус **Up** . Продолжительность, указанная после **Up** , — это время работы контейнера.
```
docker ps -a -f=name='kube-apiserver|kube-controller-manager|kube-scheduler'
```
Пример вывода:
```
CONTAINER ID        IMAGE                                COMMAND                  CREATED             STATUS              PORTS               NAMES
26c7159abbcc        rancher/hyperkube:v1.11.5-rancher1   "/opt/rke-tools/en..."   3 hours ago         Up 3 hours                              kube-apiserver
f3d287ca4549        rancher/hyperkube:v1.11.5-rancher1   "/opt/rke-tools/en..."   3 hours ago         Up 3 hours                              kube-scheduler
bdf3898b8063        rancher/hyperkube:v1.11.5-rancher1   "/opt/rke-tools/en..."   3 hours ago         Up 3 hours                              kube-controller-manager
```

# Логирование контейнера Controlplane

***Примечание.** Если вы добавили в разные  ноды с controlplane, оба kube-controller-manager и kube-scheduler будут использовать процесс выбора лидера для определения лидера. Только текущий лидер будет регистрировать выполненные действия. См. [Выборы лидера Kubernetes](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/troubleshooting/kubernetes-components/controlplane/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/troubleshooting/kubernetes-resources/#kubernetes-leader-election) , как получить текущего лидера.*

Журнал контейнеров может содержать информацию о том, в чем может быть проблема.
```
docker logs kube-apiserver
docker logs kube-controller-manager
docker logs kube-scheduler
```

# Ведение журнала сервера RKE2

Если Rancher инициализирует кластер RKE2, который не может взаимодействовать с Rancher, вы можете запустить эту команду на узле сервера в нижестоящем кластере, чтобы получить журналы сервера RKE2:
```
journalctl -u rke2-server -f
```
