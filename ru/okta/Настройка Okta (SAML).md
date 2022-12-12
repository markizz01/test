


|**Название**|**Вес**|
| :- | :- |
|<p>[Configuring Okta (SAML)](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/okta/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/okta/_index.md") </p><p>Настройка Okta (SAML)[^1]</p>|1210|


#### [Предварительные требования](https://github.com/markizz01/test/blob/main/ru/okta/Настройка%20Okta%20(SAML).md#предварительные-требования-1)

#### [Настройка Okta в Rancher]


Если ваша организация использует Okta Identity Provider (IdP) для аутентификации пользователей, вы можете настроить Rancher так, чтобы ваши пользователи могли входить в систему, используя свои учетные данные IdP.

***Примечание:** Интеграция с Okta поддерживает только логины, инициированные поставщиком услуг (Service Provider).*
# Предварительные требования
  В Okta создайте приложение SAML с приведенными ниже настройками. Обратитесь за помощью к [документации Okta](https://developer.okta.com/standards/SAML/setting_up_a_saml_application_in_okta "https://developer.okta.com/standards/SAML/setting_up_a_saml_application_in_okta").


|**Параметр**|**Значение**|
| :-: | :-: |
|Single Sign on URL|https://yourRancherHostURL/v1-saml/okta/saml/acs|
|Audience URI (SP Entity ID)|https://yourRancherHostURL/v1-saml/okta/saml/metadata|

# Настройка Okta в Rancher
1. В левом верхнем углу нажмите **☰> Users & Authentication** (пользователи и аутентификация).
1. В левом навигационном меню выберите **Auth Provider** (поставщик аутентификации).
1. Нажмите **Okta**.
1. Заполните форму **Configure Okta Account** (настройка учетной записи Okta). Приведенные ниже примеры описывают, как вы можете сопоставить с полями в Rancher атрибуты Okta из операторов атрибутов.



|**Поле**|**Описание**|
| :-: | :-: |
|Display Name Field|Имя атрибута (из оператора атрибутов), содержащего отображаемое имя пользователей.|
|User Name Field|Имя атрибута (из оператора атрибутов), который содержит имя пользователя/заданное имя (given name).|
|UID Field|Уникальное для каждого пользователя имя атрибута (из оператора атрибутов).|
|Groups Field|Имя атрибута (в операторе атрибутов группы), который предоставляет доступ к вашим группам.|
|Rancher API Host|URL-адрес вашего сервера Rancher.|
|Private Key / Certificate|Пара ключ/сертификат, используемая для шифрования утверждений (Assertion Encryption).|
|Metadata XML|Файл Identity Provider metadata, который вы найдете в разделе Sign On (вход в приложение).|

  ***Совет:** Вы можете сгенерировать пару ключ/сертификат с помощью команды openssl. Например:*

*openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout myservice.key -out myservice.crt*

1. После заполнения формы **Configure Okta Account** (настройка учетной записи Okta) нажмите **Enable** (включить).

Rancher перенаправляет вас на страницу входа в систему IdP. Введите учетные данные, которые проверяют подлинность с помощью Okta IdP, чтобы провалидировать вашу конфигурацию Rancher Okta.

***Примечание:** Если кажется, что ничего не происходит, скорее всего, причина этого в том, что ваш браузер заблокировал всплывающее окно. Убедитесь, что вы отключили блокировщик всплывающих окон для своего домена rancher и внесли его в белый список любых других расширений, которые вы можете использовать.*

#### **Результат:** Rancher настроен для работы с Okta. Теперь ваши пользователи могут входить в Rancher с помощью своих логинов из Okta.

{{< saml\_caveats >}}


