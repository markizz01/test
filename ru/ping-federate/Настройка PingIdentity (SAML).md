


|**Название**|**Вес**|
| :- | :- |
|<p> </p><p>Настройка PingIdentity (SAML)[^1][^2][^3]</p>|1200|


Если ваша организация использует Ping Identity Provider (IdP) для аутентификации пользователей, вы можете настроить Rancher так, чтобы ваши пользователи могли входить в систему, используя свои учетные данные IdP.



***Предварительные требования:***

- *У вас должен быть настроен [сервер Ping IdP](https://www.pingidentity.com/).*
- *Необходимо настроить ниже приведенные URL-адреса поставщика услуг Rancher (Rancher Service Provider):* 
  - *URL метаданных: https://<rancher-server>/v1-saml/ping/saml/metadata* 
  - *Assertion Consumer Service (ACS) URL: https://<rancher-server>/v1-saml/ping/saml/acs* 
*Обратите внимание, что эти URL-адреса не будут возвращать валидные данные до тех пор, пока настройки аутентификации не будут сохранены в Rancher.*
- *Экспортируйте файл metadata.xml с вашего сервера IdP. Для получения дополнительной информации см. [документацию по PingIdentity](https://documentation.pingidentity.com/pingfederate/pf83/index.shtml#concept_exportingMetadata.html)

1. В левом верхнем углу нажмите **☰> Users & Authentication** (пользователи и аутентификация).
2. В левом навигационном меню выберите **Auth Provider** (поставщик аутентификации).
3. Нажмите **Ping Identity**.
4. Заполните форму **Configure a Ping Account** (настройки учетной записи Ping). Ping IdP позволяет вам указать, какое хранилище данных вы хотите использовать. Вы можете либо добавить базу данных, либо использовать существующий ldap-сервер. Если вы выберете сервер Active Directory (AD), ознакомьтесь с приведенными ниже примерами, чтобы узнать, как сопоставить атрибуты AD с полями в Rancher.
    1. **Display Name Field**: Введите атрибут AD, содержащий отображаемые имена пользователей (пример: displayName).
    2. **User Name Field**: Введите атрибут AD, содержащий имя пользователя/заданное имя (given name). Например, givenName.
    3. **UID Field**: Введите атрибут AD, уникальный для каждого пользователя (пример: sAMAccountName, distinguishedName).
    4. **Groups Field**: Вносит записи для управления членством в группах (пример: memberOf).
    5. **Entity ID Field** (необязательно): опубликованный уникальный идентификатор вашего партнера, зависящий от протокола. Этот идентификатор определяет вашу организацию как объект, управляющий сервером для транзакций SAML 2.0. Этот идентификатор, возможно, был получен вне диапазона или через файл метаданных SAML.
    6. **Rancher API Host**: введите URL-адрес вашего сервера Rancher.
    7. **Private Key and Certificate**: пара ключ-сертификат для создания защищенной оболочки (secure shell) между Rancher и вашим IdP.
Вы можете сгенерировать ее с помощью команды openssl. Например:
openssl req -x509 -newkey rsa:2048 -keyout myservice.key -out myservice.cert -days 365 -nodes -subj "/CN=myservice.example.com"
    8. **IDP-metadata**: файл metadata.xml, который вы экспортировали с вашего [сервера IdP](https://documentation.pingidentity.com/pingfederate/pf83/index.shtml#concept_exportingMetadata.html "https://documentation.pingidentity.com/pingfederate/pf83/index.shtml#concept_exportingMetadata.html").
5. После заполнения формы **Configure Ping Account** нажмите **Enable** (включить).

Rancher перенаправляет вас на страницу входа в систему IdP. Чтобы провалидировать вашу конфигурацию Rancher PingIdentity, введите учетные данные, необходимые для аутентификации с помощью Ping IdP.

***Примечание:** Возможно, вам придется отключить блокировщик всплывающих окон, чтобы увидеть страницу входа в IdP.*

**Результат:** Rancher настроен для работы с PingIdentity. Теперь ваши пользователи могут входить в Rancher, используя свои логины PingIdentity.

{{< saml\_caveats >}}









[^1]: [Configuring](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/ping-federate/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/ping-federate/_index.md")
[^2]: [PingIdentity](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/ping-federate/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/ping-federate/_index.md")
[^3]: [SAML](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/ping-federate/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/ping-federate/_index.md")
