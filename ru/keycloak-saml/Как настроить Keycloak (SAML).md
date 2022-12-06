


|**Название**|**Описание**|**Вес**|
| :- | :- | :- |
|<p>[Configuring Keycloak (SAML)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/keycloak-saml/_index.md) </p><p>Как настроить Keycloak (SAML)[^1]</p>|Создайте клиент Keycloak SAML и настройте Rancher для работы с Keycloak. В результате ваши пользователи смогут войти в Rancher, используя свои логины Keycloak.|1200|


[**Предварительные требования](#_7i9epremx5h9)	**1****

[**Получение метаданных IDP](#_rq5ypx6dg3n)	**4****

[**Как настроить Keycloak в Rancher](#_gav3c7qm12ds)	**6****

[**Справка по конфигурированию](#_jdrojqmap2zd)	**6****

[**Приложение: Устранение неполадок](#_xy2szy4zb16d)	**7****

[Не произошло перенаправление на Keycloak](#_qt7d9evgk2pl)	7

[После входа в систему IdP отображается сообщение Forbidden](#_103ykebn9bh7)	8

[HTTP 502 при попытке получить доступ к /v1-saml/keycloak/saml/metadata](#_43m0pisosbjk)	8

[Ошибка Keycloak: "We're sorry, failed to process response"](#_64ym9apa5g36)	8

[Ошибка Keycloak: "We're sorry, invalid requester"](#_9wut05h29u6w)	8


Если ваша организация использует Keycloak Identity Provider (IdP) для аутентификации пользователей, вы можете настроить Rancher так, чтобы ваши пользователи могли входить в систему, используя свои учетные данные IdP.
# Предварительные требования
- У вас должен быть настроен [IdP-сервер Keycloak](https://www.keycloak.org/docs/latest/server_installation/).
- В Keycloak создайте [новый SAML-клиент](https://www.keycloak.org/docs/latest/server_admin/#oidc-clients) с приведенными ниже настройками. Для получения дополнительной информации обратитесь к [документации по Keycloak](https://www.keycloak.org/docs/latest/server_admin/#saml-clients).


|**Параметр**|**Значение**|
| :-: | :-: |
|Sign Documents|On[1](#b4xdzpmtoe7)|
|Sign Assertions|On[1](#b4xdzpmtoe7)|
|Все остальные параметры с On/Off|Off|
|Client ID|Либо https://yourRancherHostURL/v1-saml/keycloak/saml/metadata, либо значение, настроенное в Entry ID Field (поле идентификатора входа) в Keycloak-настройке Rancher[2](#fb6lnzucojvd)|
|Client Name|<CLIENT\_NAME> (например, 'rancher')|
|Client Protocol|SAML|
|Valid Redirect URI|https://yourRancherHostURL/v1-saml/keycloak/saml/acs|

\1.  При желании вы можете включить один или оба этих параметра. 

\2. SAML-метаданные Rancher не будут сгенерированы до тех пор, пока поставщик SAML (SAML provider) не будет настроен и сохранен.

![](Aspose.Words.afc399d7-196c-4f7f-b979-ad22f162deef.001.png)

- В новом SAML-клиенте создайте несколько Mapper для отображения пользовательских полей:
  - Добавьте все "Builtin Protocol Mappers" (Mapper встроенного протокола)

![](Aspose.Words.afc399d7-196c-4f7f-b979-ad22f162deef.002.png)

- Создайте новый Mapper "Group list" (список групп), чтобы сопоставить атрибут участника с группами пользователя

![](Aspose.Words.afc399d7-196c-4f7f-b979-ad22f162deef.003.png)
# Получение метаданных IDP
- [*Keycloak 5 и более ранние версии*](#sw0e5kj4h55l)
- [*Keycloak 6-13*](#da9sizovw7f6)
- [*Keycloak 14+*](#z8zc2tc373fv)

*Keycloak 5 и более ранние версии*

`	`Чтобы получить метаданные IDP, экспортируйте файл metadata.xml из вашего клиента Keycloak. На вкладке **Installation** (установка) выберите опцию форматирования **SAML Metadata IDPSSODescriptor** и загрузите свой файл.

*Keycloak 6-13*

1. В разделе **Configure** (настройка) перейдите на вкладку **Realm Settings** (параметры области безопасности).
1. Перейдите на вкладку **General** (общие).
1. В поле **Endpoints** (конечные точки) выберите **SAML 2.0 Identity Provider Metadata** (метаданные поставщика удостоверений SAML 2.0).

`	`Убедитесь, что метаданные IDP содержат следующие атрибуты:

xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata"

xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"

xmlns:ds="http://www.w3.org/2000/09/xmldsig#"

`	`Некоторые браузеры, такие как Firefox, могут отображать/обрабатывать документ так, что содержимое кажется измененным, а некоторые атрибуты кажутся отсутствующими. В этой ситуации используйте исходные данные ответа, которые можно найти с помощью вашего браузера.

`	`Ниже приведен пример процесса для Firefox. Для других браузеров он будет немного отличаться:

1. Нажмите **F12**, чтобы получить доступ к консоли разработчика.
1. Перейдите на вкладку **Network** (сеть).
1. В таблице нажмите строку, содержащую descriptor.
1. На панели сведений перейдите на вкладку **Response** (ответ).
1. Скопируйте исходные данные ответа.

`	`Полученный XML-файл содержит EntitiesDescriptor в качестве корневого элемента. Rancher ожидает, что корневым элементом будет EntityDescriptor, а не EntitiesDescriptor. Поэтому, прежде чем передавать этот XML в Rancher, выполните следующие действия, чтобы настроить его:

1. Скопируйте из EntitiesDescriptor в EntityDescriptor все атрибуты, которые отсутствуют.
1. Удалите тег <EntitiesDescriptor> из начала xml-файла.
1. Удалите </EntitiesDescriptor> из конца xml-файла.

У вас останется текст, аналогичный следующему:

<EntityDescriptor xmlns="urn:oasis:names:tc:SAML:2.0:metadata" xmlns:dsig="http://www.w3.org/2000/09/xmldsig#" entityID="https://{KEYCLOAK-URL}/auth/realms/{REALM-NAME}">

....

</EntityDescriptor>

*Keycloak 14+*

1. В разделе **Configure** (настройка) перейдите на вкладку **Realm Settings** (параметры области безопасности).
1. Перейдите на вкладку **General** (общие).
1. В поле **Endpoints** (конечные точки) выберите **SAML 2.0 Identity Provider Metadata** (метаданные поставщика удостоверений SAML 2.0).



Убедитесь, что метаданные IDP содержат следующие атрибуты:

xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata"

xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"

xmlns:ds="http://www.w3.org/2000/09/xmldsig#"

`	`Некоторые браузеры, такие как Firefox, могут отображать/обрабатывать документ таким образом, что содержимое кажется измененным, а некоторые атрибуты — отсутствующими. В этой ситуации используйте исходные данные ответа, которые можно найти с помощью вашего браузера.

`	`Ниже приведен пример процесса для Firefox. Для других браузеров он будет немного отличаться:

1. Нажмите **F12**, чтобы получить доступ к консоли разработчика.
1. Перейдите на вкладку **Network** (сеть).
1. В таблице нажмите строку, содержащую descriptor.
1. На панели сведений перейдите на вкладку **Response** (ответ).
1. Скопируйте исходные данные ответа.
# Как настроить Keycloak в Rancher
1. В левом верхнем углу нажмите **☰> Users & Authentication** (пользователи и аутентификация).
1. В левом навигационном меню выберите **Auth Provider** (поставщик аутентификации).
1. Нажмите **Keycloak SAML**.
1. Заполните форму **Configure Keycloak Account** (настройка учетной записи Keycloak). Для получения дополнительной информации по заполнению формы см. раздел [Справка по конфигурированию](#_jdrojqmap2zd).
1. После заполнения формы **Configure a Keycloak Account** нажмите **Enable** (включить).

Rancher перенаправляет вас на страницу входа в систему IdP. Введите учетные данные для аутентификации с помощью Keycloak IdP, чтобы подтвердить вашу конфигурацию Rancher Keycloak.

***Примечание:** Возможно, вам придется отключить блокировщик всплывающих окон, чтобы увидеть страницу входа IdP.*

**Результат:** Rancher настроен для работы с Keycloak. Теперь ваши пользователи могут входить в Rancher, используя свои логины Keycloak.

{{< saml\_caveats >}}

# Справка по конфигурированию


|**Поле**|**Описание**|
| :-: | :-: |
|Display Name Field|Атрибут, содержащий отображаемое имя пользователей. Пример: givenName|
|User Name Field|Атрибут, содержащий имя пользователя/заданное имя (user name/given name). Пример: email|
|UID Field|Атрибут, который уникален для каждого пользователя. Пример: email|
|Groups Field|Создает записи для управления членством в группах. Пример: member|
|Entity ID Field|<p>Идентификатор, который необходимо настроить в качестве идентификатора клиента в клиенте Keycloak.</p><p>Значение по умолчанию: https://yourRancherHostURL/v1-saml/keycloak/saml/metadata</p>|
|Rancher API Host|URL-адрес вашего сервера Rancher.|
|Private Key / Certificate|Пара ключ/сертификат для создания защищенной оболочки (secure shell) между Rancher и вашим IdP.|
|IDP-metadata|Файл metadata.xml, который вы экспортировали с вашего сервера IdP.|

***Совет:** Вы можете сгенерировать пару ключ/сертификат с помощью команды openssl. Например:*

openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout myservice.key -out myservice.cert

# Приложение: Устранение неполадок
`	`Если у вас возникли проблемы при тестировании подключения к серверу Keycloak, сначала дважды проверьте параметр конфигурации вашего SAML-клиента. Вы также можете просмотреть журналы Rancher, чтобы точно определить причину проблемы. Журналы отладки (debug log) могут содержать более подробную информацию об ошибке. Пожалуйста, обратитесь к разделу "Как я могу включить ведение журнала отладки" в этой документации.
## Не произошло перенаправление на Keycloak
`	`Когда вы нажимаете **Authenticate with Keycloak** (аутентификация с помощью Keycloak), вы не перенаправляетесь на свой IdP.

- Проверьте конфигурацию вашего клиента Keycloak.
- Убедитесь, что в Force Post Binding установлено значение OFF (выключено).
## После входа в систему IdP отображается сообщение Forbidden
`	`Вы корректно перенаправлены на страницу входа в систему IdP, и вы можете ввести свои учетные данные, однако впоследствии вы получите сообщение Forbidden (запрещено).

- Проверьте журнал отладки Rancher.
- Если в журнале отображается сообщение "ERROR: either the Response or Assertion must be signed"[^2], убедитесь, что для параметра Sign Documents или Sign assertions в вашем клиенте Keycloak установлено значение ON.

## HTTP 502 при попытке получить доступ к /v1-saml/keycloak/saml/metadata
`	`Обычно это происходит из-за того, что метаданные не создаются до тех пор, пока не будет настроен поставщик SAML (SAML provider). Попробуйте настроить и сохранить Keycloak в качестве вашего поставщика SAML, а затем получить доступ к метаданным.

## Ошибка Keycloak: "We're sorry, failed to process response"[^3]
- Проверьте свой журнал Keycloak.
- Если в журнале отображается failed: org.keycloak.common.VerificationException: Client does not have a public key[^4], установите Encrypt Assertions равным OFF (выключено) в вашем клиенте Keycloak.

## Ошибка Keycloak: "We're sorry, invalid requester"[^5]
- Проверьте свой журнал Keycloak.
- Если в журнале отображается request validation failed: org.keycloak.common.VerificationException: SigAlg was null[^6], установите Client Signature Required равным OFF в вашем клиенте Keycloak.


[^1]: 
[^2]: "ОШИБКА: либо Response, либо Assertion должны быть подписаны".
[^3]: "Извините, не удалось обработать ответ".
[^4]: "Ошибка: org.keycloak.common.VerificationException: у клиента нет открытого ключа".
[^5]: "Извините, неверный отправитель запроса".
[^6]: "Ошибка проверки запроса: исключение org.keycloak.common.VerificationException: значение SigAlg равно null".