***Примечание.** Системные инструменты устарели с июня 2022 года.*

# Журналы
Пожалуйста, используйте [logs-collector](https://github.com/rancherlabs/support-tools/tree/master/collection/rancher/v2.x/logs-collector) для сбора журналов из вашего кластера.

# Статистика
Если вы хотите воспроизвести команду stats, вы можете запустить следующую команду на узлах вашего кластера:

***Примечание.** Для этой команды требуется пакет sysstat на узле кластера.*
```
/usr/bin/sar -u -r -F 1 1
```
№ Удаление
Пожалуйста, используйте инструмент [Rancher Cleanup.](https://github.com/rancher/rancher-cleanup)
