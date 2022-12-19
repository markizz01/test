Команды/шаги, перечисленные на этой странице, можно использовать для проверки кластеров, которые вы регистрируете или которые зарегистрированы в Rancher.

Убедитесь, что вы настроили правильный kubeconfig (например, export KUBECONFIG=$PWD/kubeconfig_from_imported_cluster.yml)

# Агенты Rancher

Связь с кластером (API Kubernetes через cattle-cluster-agent) и связь с узлами осуществляется через агентов Rancher.

Если cattle-cluster-agent не может подключиться к настроенному server-url, кластер останется в состоянии ожидания , показывая Waiting for full cluster configuration.

# cattle-node-agent

***Примечание:** cattle-node-agents присутствуют только в кластерах, созданных в Rancher с помощью RKE.*

Проверьте, присутствуют ли поды cattle-node-agents на каждой нодее, имеют ли они статус « Работает » и не имеют ли большого количества перезапусков:
```
kubectl -n cattle-system get pods -l app=cattle-agent -o wide
```

Пример вывода:
```
NAME                      READY     STATUS    RESTARTS   AGE       IP                NODE
cattle-node-agent-4gc2p   1/1       Running   0          2h        x.x.x.x           worker-1
cattle-node-agent-8cxkk   1/1       Running   0          2h        x.x.x.x           etcd-1
cattle-node-agent-kzrlg   1/1       Running   0          2h        x.x.x.x           etcd-0
cattle-node-agent-nclz9   1/1       Running   0          2h        x.x.x.x           controlplane-0
cattle-node-agent-pwxp7   1/1       Running   0          2h        x.x.x.x           worker-0
cattle-node-agent-t5484   1/1       Running   0          2h        x.x.x.x           controlplane-1
cattle-node-agent-t8mtz   1/1       Running   0          2h        x.x.x.x           etcd-2
```

Проверьте ведение журнала конкретного пода cattle-node-agents или всех подов cattle-node-agents:
```
kubectl -n cattle-system logs -l app=cattle-agent
cattle-cluster-agent
```

Проверьте, присутствует ли под cattle-cluster-agent в кластере, имеет ли он статус « Работает » и не имеет ли большого количества перезапусков:
```
kubectl -n cattle-system get pods -l app=cattle-cluster-agent -o wide
```

Пример вывода:
```
NAME                                    READY     STATUS    RESTARTS   AGE       IP           NODE
cattle-cluster-agent-54d7c6c54d-ht9h4   1/1       Running   0          2h        x.x.x.x      worker-1
```

Проверьте ведение журнала группы cattle-cluster-agent:
```
kubectl -n cattle-system logs -l app=cattle-cluster-agent
```
