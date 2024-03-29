﻿


|**Название**|**Вес**|
| :- | :- |
|<p>Справка по настройке OpenLDAP[^1]</p>|2|


1.  [**Справочная информация: Процесс аутентификации с помощью OpenLDAP**]

2.  [**Настройка сервера OpenLDAP**]

3.  [**Настройка схемы пользователя/группы**]

    + [Настройка схемы пользователя]

    + [Настройка схемы группы]


Этот раздел предназначен для использования в качестве справочного материала при настройке поставщика аутентификации OpenLDAP в Rancher.

Для получения более подробной информации о настройке OpenLDAP обратитесь к [официальной документации](https://www.openldap.org/doc/ "https://www.openldap.org/doc/").

*Прежде чем приступить к настройке, пожалуйста, ознакомьтесь с концепциями из раздела "Внешняя настройка аутентификации и пользователи-принципалы (principal user)".*

# Справочная информация: Процесс аутентификации с помощью OpenLDAP
1. Когда пользователь пытается войти в систему с учетными данными LDAP, Rancher создает первоначальное подключение (bind) к серверу LDAP, используя учетную запись сервиса с разрешениями на поиск в директории и чтение атрибутов пользователя/группы.
2. Затем Rancher выполняет поиск пользователя в каталоге, используя фильтр поиска на основе предоставленного имени пользователя и настроенных сопоставлений атрибутов.
3. Сразу после того, как пользователь будет найден, он пройдет аутентификацию с помощью другого запроса на подключение (bind request) в LDAP, для этого будет использован DN пользователя и предоставленный пароль.
4. Сразу после того, как аутентификация пройдет успешно, Rancher произведет урегулирование членства в группах как с помощью атрибута членства в объекте пользователя, так и путем выполнения поиска группы (group search) на основе настроенного атрибута сопоставления пользователя.

# Настройка сервера OpenLDAP
Вам нужно будет ввести адрес, порт и протокол для подключения к вашему серверу OpenLDAP. 389 — это стандартный порт для незащищенного трафика (insecure traffic), 636 — для трафика TLS.

***Использование TLS?***

*Если сертификат, используемый сервером OpenLDAP, является самоподписанным (self-signed) или получен не от общепризнанного центра сертификации, убедитесь, что у вас под рукой есть сертификат CA (объединенный с любыми промежуточными сертификатами) в формате PEM. Вам нужно будет вставить этот сертификат во время настройки, чтобы Rancher мог проверить цепочку сертификатов.*

`	`Если вы сомневаетесь в правильности ввода значений в поля конфигурации базы поиска пользователя/группы, свяжитесь со своим администратором LDAP или обратитесь к разделу документации "Определите базу поиска и схему с помощью ldapsearch, описывающему аутентификацию с помощью Active Directory.

Параметры сервера OpenLDAP

|**Параметр**|**Описание**|
| :-: | :-: |
|Hostname|Задает имя хоста или IP-адрес сервера OpenLDAP|
|Port|Задает порт, на котором сервер OpenLDAP прослушивает соединения. Незашифрованный LDAP обычно использует стандартный порт 389, в то время как LDAPS использует порт 636.|
|TLS|Установите этот флаг, чтобы включить LDAP с использованием SSL/TLS (обычно известный как LDAPS). Вам также нужно будет вставить сертификат CA, если сервер использует самоподписанный сертификат (self-signed certificate) или сертификат с корпоративной подписью (enterprise-signed certificate).|
|Server Connection Timeout|Продолжительность времени (в секундах), которое Rancher ожидает, прежде чем принять решение о недоступности сервера.|
|Service Account Distinguished Name|Введите уникальное имя (Distinguished Name, DN) пользователя, которое следует использовать для подключения (bind), поиска и извлечения LDAP-записей.|
|Service Account Password|Пароль для учетной записи сервиса.|
|User Search Base|<p>Введите уникальное имя (Distinguished Name, DN) узла в вашем дереве каталогов, с которого следует начать поиск объектов пользователя. Все пользователи должны быть потомками этого базового DN. </p><p>Например: "ou=people,dc=acme, dc=com".</p>|
|Group Search Base|Если ваши группы находятся под другим узлом, чем тот, который настроен в User Search Base (база поиска пользователей), вам нужно будет указать здесь уникальное имя (Distinguished Name, DN). В противном случае оставьте это поле пустым. Например: "ou=groups,dc=acme,dc=com".|

# Настройка схемы пользователя/группы
Если ваш каталог OpenLDAP отличается от стандартной схемы OpenLDAP, вы должны заполнить раздел **Customize Schema** (настройка схемы), чтобы установить соответствие между ними.

Обратите внимание, что сопоставления атрибутов, настроенные в этом разделе, используются Rancher для построения фильтров поиска и разрешения членства в группах. Поэтому всегда рекомендуется проверять, что приведенная здесь конфигурация соответствует схеме, используемой в вашем OpenLDAP.

Если вы не знакомы со схемой пользователя/группы, используемой на сервере OpenLDAP, проконсультируйтесь с вашим администратором LDAP или обратитесь к разделу документации "Определите базу поиска и схему с помощью ldapsearch", описывающему аутентификацию с помощью Active Directory.

## Настройка схемы пользователя
В таблице ниже подробно описаны параметры для настройки пользовательской схемы.

Параметры настройки схемы пользователя

|**Параметр**|**Описание**|
| :-: | :-: |
|Object Class|Имя класса объектов, используемого для объектов пользователя в вашем домене. Если определено, укажите только имя класса объекта — не включайте его в обертку LDAP (LDAP wrapper), такую как &(objectClass=xxxx)|
|Username Attribute|Атрибут пользователя, значение которого подходит в качестве отображаемого имени.|
|Login Attribute|Атрибут, значение которого соответствует фрагменту имени пользователя учетных данных, введенных вашими пользователями при входе в Rancher. Обычно это uid.|
|User Member Attribute|Атрибут пользователя, содержащий уникальное имя (Distinguished Name, DN) групп, членом которых является пользователь. Обычно это memberOf или isMemberOf.|
|Search Attribute|Когда пользователь вводит текст для добавления пользователей или групп в пользовательский интерфейс, Rancher отправляет запрос на сервер LDAP и пытается произвести сопоставление пользователей с помощью атрибутов, указанных в этом параметре. Можно указать несколько атрибутов, разделив их символом канала ("|").|
|User Enabled Attribute|Если схема вашего сервера OpenLDAP поддерживает атрибут пользователя, значение которого можно вычислить, чтобы определить, отключена ли или заблокирована ли учетная запись, введите имя этого атрибута. По умолчанию схема OpenLDAP не поддерживает это поведение, и данное поле обычно следует оставлять пустым.|
|Disabled Status Bitmask|Это значение для отключенной/заблокированной учетной записи пользователя. Параметр игнорируется, если User Enabled Attribute пуст.|

## Настройка схемы группы
В таблице ниже подробно описаны параметры для настройки схемы группы.


|**Параметр**|**Описание**|
| :-: | :-: |
|Object Class|Название класса объектов, используемое для групповых записей в вашем домене. Если определено, укажите только имя класса объекта — не включайте его в обертку LDAP (LDAP wrapper), такую как &(objectClass=xxxx)|
|Name Attribute|Атрибут группы, значение которого подходит для отображаемого имени.|
|Group Member User Attribute|Имя **атрибута пользователя**, формат которого соответствует членам группы в Group Member Mapping Attribute.|
|Group Member Mapping Attribute|Название атрибута группы, содержащего членов группы.|
|Search Attribute|Атрибут, используемый для создания фильтров поиска при добавлении групп в кластеры или проекты в пользовательском интерфейсе. Смотрите описание в схеме пользователя (Search Attribute).|
|Group DN Attribute|Название атрибута группы, формат которого соответствует значениям в атрибуте членства пользователя в группе. Смотрите User Member Attribute.|
|Nested Group Membership|Эти параметры определяют, должен ли Rancher разрешать членство во вложенных группах. Используйте только в том случае, если ваша организация использует эти вложенные членства (т.е. у вас есть группы, которые содержат другие группы в качестве участников). Эта опция отключена, если вы используете Shibboleth.|




[^1]: [OpenLDAP Configuration Reference](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/openldap/openldap-config/_index.md "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/openldap/openldap-config/_index.md")
