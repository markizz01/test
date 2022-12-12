


|**Название**|**Вес**|
| :- | :- |
|<p>[Configuring Microsoft Active Directory Federation Service (SAML)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/microsoft-adfs/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/microsoft-adfs/_index.md") </p><p>Настройка Microsoft Active Directory Federation Service (SAML)[^1]</p>|1205|


### [Предварительные требования](https://github.com/markizz01/test/blob/main/ru/microsoft-adfs/Настройка%20Microsoft%20Active%20Directory%20Federation%20Service%20(SAML).md#предварительные-требования-1)

### [Схема настройки](https://github.com/markizz01/test/blob/main/ru/microsoft-adfs/Настройка%20Microsoft%20Active%20Directory%20Federation%20Service%20(SAML).md#схема-настройки-1)

Если ваша организация использует Microsoft Active Directory Federation Services (AD FS) для аутентификации пользователей, вы можете настроить Rancher так, чтобы ваши пользователи могли входить в систему, используя свои учетные данные AD FS.
# Предварительные требования
У вас должен быть установлен Rancher.

- Получите URL-адрес вашего сервера Rancher. Во время настройки AD FS замените этот URL-адрес на временный местозаполнитель <RANCHER\_SERVER>.
- Убедитесь, что у вас есть учетная запись глобального администратора в вашей установке Rancher.

У вас должен быть настроен сервер [Microsoft AD FS](https://docs.microsoft.com/en-us/windows-server/identity/active-directory-federation-services "https://docs.microsoft.com/en-us/windows-server/identity/active-directory-federation-services").

- Получите IP-адрес вашего сервера AD FS или его DNS-имя. Во время настройки AD FS замените этот IP-адрес (DNS-имя) на временный местозаполнитель <AD\_SERVER>.
- Убедитесь, что у вас есть доступ к добавлению [объектов ](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/create-a-relying-party-trust "https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/create-a-relying-party-trust")[*Relying Party Trust*](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/create-a-relying-party-trust "https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/create-a-relying-party-trust") на вашем сервере AD FS.
# Схема настройки
  Для того, чтобы настроить в Rancher аутентификацию с помощью Microsoft AD FS, необходимо настроить AD FS на вашем сервере Active Directory и настроить Rancher для использования вашего сервера AD FS. На следующих страницах описаны шаги, необходимые для настройки Microsoft AD FS в вашей установке Rancher.

- 1. [Настройка Microsoft AD FS для Rancher](https://github.com/markizz01/test/blob/main/ru/microsoft-adfs/microsoft-adfs-setup/1.%20Настройка%20Microsoft%20AD%20FS%20для%20Rancher.md)
- 2. Настройка Rancher для Microsoft AD FS.

{{< saml\_caveats >}}

Далее: [Настройка Microsoft AD FS для Rancher](https://github.com/markizz01/test/blob/main/ru/microsoft-adfs/microsoft-adfs-setup/1.%20Настройка%20Microsoft%20AD%20FS%20для%20Rancher.md)


