Для версий Rancher в которых установлен rancher-webhook некоторые версии создали сертификаты, срок действия которых истекает через год. Вам необходимо будет сменить сертификат webhook, если сертификат не был обновлен.
В Rancher v2.6.3 и выше развертывания rancher-webhook автоматически обновляют свой сертификат TLS, когда до истечения срока его действия остается не более 30 дней. Если вы используете версию 2.6.2 или более раннюю, есть два способа обойти эту проблему:

**1. Пользователи с доступом к кластеру выполните следующие команды:**
```
kubectl delete secret -n cattle-system cattle-webhook-tls
kubectl delete mutatingwebhookconfigurations.admissionregistration.k8s.io --ignore-not-found=true rancher.cattle.io
kubectl delete pod -n cattle-system -l app=rancher-webhook
```

**2. Пользователи без доступа к кластеру через kubectl:**

1.	Удалите cattle-webhook-tls  в cattle-system в локальном кластере.
2.	Удалите изменяющийся вебхук rancher.cattle.io 
3.	Удалите под rancher-webhook в cattle-system в локальном кластере.


***Примечание.** Проблема с истечением срока действия сертификата вебхука не относится к cattle-webhook-tls,  перечисленным в примерах. Соответственно Вы заполните свой секретный сертификат с истекшим сроком действия.*
