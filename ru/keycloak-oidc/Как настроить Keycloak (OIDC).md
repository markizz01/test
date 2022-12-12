


|**Название**|**Описание**|**Вес**|
| :- | :- | :- |
|<p>[Configuring Keycloak (OIDC)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/keycloak-oidc/_index.md) </p><p>Как настроить Keycloak (OIDC)[^1]</p>|Создайте клиент Keycloak OpenID Connect (OIDC) и настройте Rancher для работы с Keycloak. В результате ваши пользователи смогут войти в Rancher, используя свои логины Keycloak.|1200|


### [Предварительные требования](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#предварительные-требования)

### [Как настроить Keycloak в Rancher](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#как-настроить-keycloak-в-rancher-1)

### [Справка по конфигурированию](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#справка-по-конфигурированию-1)

### [Переход с SAML на OIDC](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#переход-с-saml-на-oidc-1)

[Перенастройка Keycloak](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#перенастройка-rancher)

[Перенастройка Rancher](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#перенастройка-rancher)

### [Приложение: Устранение неполадок](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#приложение-устранение-неполадок-1)

[Не произошло перенаправление на Keycloak](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#не-произошло-перенаправление-на-keycloak)

[Сгенерированные Issuer и Auth Endpoint некорректны](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#сгенерированные-issuer-и-auth-endpoint-некорректны)

[Ошибка Keycloak: "Invalid grant_type"](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#ошибка-keycloak-invalid-grant_type)

  Если ваша организация использует [Keycloak Identity Provider (IdP)](https://www.keycloak.org/) для аутентификации пользователей, вы можете настроить Rancher так, чтобы ваши пользователи могли входить в систему, используя свои учетные данные IdP. Rancher поддерживает интеграцию с Keycloak с использованием протокола OpenID Connect (OIDC) и протокола SAML. Обе реализации функционально эквивалентны при использовании с Rancher. На этой странице описывается процесс настройки Rancher для работы с Keycloak с использованием протокола OIDC.

  Если вы предпочитаете вместо этого использовать Keycloak с протоколом SAML, обратитесь к этой странице.

  Если у вас есть существующая конфигурация, использующая протокол SAML, и вы хотите переключиться на протокол OIDC, обратитесь к [этому разделу](#_p6wz4137ggp5).
# Предварительные требования
- В Rancher должен быть отключен Keycloak (SAML).
- У вас должен быть настроен [IdP-сервер Keycloak](https://www.keycloak.org/docs/latest/server_installation/).
- В Keycloak создайте [нового клиента OIDC](https://www.keycloak.org/docs/latest/server_admin/#oidc-clients) с приведенными ниже настройками. Для получения дополнительной информации обратитесь к [документации Keycloak](https://www.keycloak.org/docs/latest/server_admin/#oidc-clients).


|**Параметр**|**Значение**|
| :-: | :-: |
|Client ID|<CLIENT\_ID> (e.g. rancher)|
|Name|<CLIENT\_NAME> (e.g. rancher)|
|Client Protocol|openid-connect|
|Access Type|confidential|
|Valid Redirect URI|https://yourRancherHostURL/verify-auth|

- В новом клиенте OIDC создайте несколько [Mapper](https://www.keycloak.org/docs/latest/server_admin/#_protocol-mappers) для отображения пользовательских полей.
  - Создайте новый Mapper "Groups Mapper" (Mapper группы) с приведенными ниже настройками.


|**Параметр**|**Значение**|
| :-: | :-: |
|Name|Groups Mapper|
|Mapper Type|Group Membership|
|Token Claim Name|groups|
|Add to ID token|OFF|
|Add to access token|OFF|
|Add to user info|ON|

- Создайте новый Mapper "Client Audience" (клиентская аудитория) с настройками, приведенными ниже.



|**Параметр**|**Значение**|
| :-: | :-: |
|Name|Client Audience|
|Mapper Type|Audience|
|Included Client Audience|<CLIENT\_NAME>|
|Add to access token|ON|

- Создайте новый Mapper "Groups Path" (путь группы) с приведенными ниже настройками.


|**Параметр**|**Значение**|
| :-: | :-: |
|Name|Group Path|
|Mapper Type|Group Membership|
|Token Claim Name|full\_group\_path|
|Full group path|ON|
|Add to user info|ON|
# Как настроить Keycloak в Rancher
1. В пользовательском интерфейсе Rancher нажмите **☰> Users & Authentication** (пользователи и аутентификация).
1. В левом навигационном меню выберите **Auth Provider** (поставщик аутентификации).
1. Нажмите **Keycloak (OIDC)**.
1. Заполните форму **Configure a Keycloak OIDC account** (настройка учетной записи OIDC Keycloak). Для получения дополнительной информации по заполнению формы см. раздел [Справка по конфигурированию](https://github.com/markizz01/test/blob/main/ru/keycloak-oidc/Как%20настроить%20Keycloak%20(OIDC).md#_drq1k1ix40gw).
1. После того, как вы заполните форму **Configure a Keycloak OIDC account**, нажмите **Enable** (включить).

  Rancher перенаправит вас на страницу входа в систему IdP. Для проверки вашей конфигурации Rancher Keycloak введите учетные данные, которые требуются для аутентификации с помощью Keycloak IdP.

***Примечание:** Возможно, вам потребуется отключить блокировщик всплывающих окон, чтобы увидеть страницу входа IdP.*

**Результат:** Rancher настроен для работы с помощью Keycloak с использованием протокола OIDC. Теперь ваши пользователи могут входить в Rancher, используя свои логины Keycloak.

# Справка по конфигурированию

|**Поле**|**Описание**|
| :-: | :-: |
|Client ID|Client ID (идентификатор клиента) вашего клиента Keycloak.|
|Client Secret|Сгенерированный Secret (секрет) вашего клиента Keycloak. В консоли Keycloak выберите **Clients** (клиенты), выберите созданного вами клиента, перейдите на вкладку **Credentials** (учетные данные) и скопируйте значение поля Secret.|
|Private Key / Certificate|Пара ключ/сертификат для создания защищенной оболочки (secure shell) между Rancher и вашим IdP. Требуется, если на вашем сервере Keycloak включен HTTPS/SSL.|
|Endpoints|Выберите, следует ли использовать для полей Rancher URL, Issue и Auth Endpoint сгенерированные значения или их необходимо переопределить вручную (если они неверны).|
|Keycloak URL|URL-адрес вашего сервера Keycloak.|
|Keycloak Realm|Имя области безопасности (realm), в которой был создан клиент Keycloak.|
|Rancher URL|URL-адрес вашего сервера Rancher.|
|Issuer|URL вашего IdP.|
|Auth Endpoint|URL-адрес, по которому пользователи перенаправляются для аутентификации.|

# Переход с SAML на OIDC
  В этом разделе описан процесс перехода от использования Keycloak (SAML) к Keycloak (OIDC).
## Перенастройка Keycloak
1. Измените существующий клиент на использование протокола OIDC. В консоли Keycloak выберите **Clients** (клиенты), выберите SAML-клиент для миграции, перейдите на вкладку **Settings** (настройки), измените Client Protocol (протокол клиента) с saml на openid-connect и нажмите **Save** (сохранить).
1. Убедитесь, что Valid Redirect URIs (корректные URI перенаправления) все еще действительны.
1. Выберите вкладку **Mappers** и создайте новый Mapper с приведенными ниже настройками.


|**Параметр**|**Значение**|
| :-: | :-: |
|Name|Groups Mapper|
|Mapper Type|Group Membership|
|Token Claim Name|groups|
|Add to ID token|ON|
|Add to access token|ON|
|Add to user info|ON|

## Перенастройка Rancher
  Перед настройкой Rancher для использования Keycloak (OIDC) сначала необходимо отключить Keycloak (SAML).

1. В пользовательском интерфейсе Rancher нажмите **☰> Users & Authentication** (пользователи и аутентификация).
1. В левом навигационном меню выберите **Auth Provider** (поставщик аутентификации).
1. Нажмите **Keycloak (SAML)**.
1. Нажмите **Disable** (отключить).

  Настройте Rancher для использования Keycloak (OIDC), выполнив действия, описанные в [этом разделе](#_gav3c7qm12ds).

***Примечание:** После завершения настройки необходимо будет повторно применить разрешения (permission) пользователя Rancher, поскольку они не переносятся автоматически.*
# Приложение: Устранение неполадок
  Если у вас возникли проблемы при тестировании подключения к серверу Keycloak, сначала дважды проверьте параметры конфигурации вашего клиента OIDC. Вы также можете просмотреть журналы Rancher, чтобы более точно определить, что вызывает проблемы. Журналы отладки (debug logs) могут содержать более подробную информацию об ошибке. Пожалуйста, обратитесь к разделу "Как я могу включить ведение журнала отладки" в этой документации.

  Все записи журнала, связанные с Keycloak, будут предваряться либо [generic oidc], либо [keycloak oidc].
## Не произошло перенаправление на Keycloak
  Когда вы заполняете форму **Configure a Keycloak OIDC account** (настройка учетной записи OIDC Keycloak) и нажимаете **Enable** (включить), вы не перенаправляетесь на свой IdP.

- Проверьте конфигурацию вашего клиента Keycloak.

## Сгенерированные Issuer и Auth Endpoint некорректны
- В форме **Configure a Keycloak OIDC account** (настройка учетной записи Keycloak OIDC) измените **Endpoints** (конечные точки) на Specify (advanced) и переопределите значения Issuer и Auth Endpoint. Чтобы найти значения, перейдите в консоль Keycloak и выберите **Realm Settings** (настройки области безопасности), выберите вкладку **General** (общие) и нажмите **OpenID Endpoint Configuration** (настройка конечной точки OpenID). В выходных данных JSON будут отображаться значения для issuer и authorization\_endpoint.
## Ошибка Keycloak: "Invalid grant\_type"
- В некоторых случаях это сообщение об ошибке может вводить в заблуждение и на самом деле быть вызвано неправильной установкой Valid Redirect URI (корректных URI перенаправления).





[^1]: 
