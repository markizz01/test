﻿


|**Название**|**Вес**|
| :- | :- |
|<p>Групповые разрешения (Group Permissions) с помощью Shibboleth и OpenLDAP[^1]</p>|1|


1.  [**Терминология**](https://github.com/markizz01/test/blob/main/ru/shibboleth/about/%D0%93%D1%80%D1%83%D0%BF%D0%BF%D0%BE%D0%B2%D1%8B%D0%B5%20%D1%80%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D1%8F%20(Group%20Permissions)%20%D1%81%20%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E%20Shibboleth%20%D0%B8%20OpenLDAP.md#%D1%82%D0%B5%D1%80%D0%BC%D0%B8%D0%BD%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F)
2.  [**Добавление групповых разрешений OpenLDAP к ресурсам Rancher**](https://github.com/markizz01/test/blob/main/ru/shibboleth/about/%D0%93%D1%80%D1%83%D0%BF%D0%BF%D0%BE%D0%B2%D1%8B%D0%B5%20%D1%80%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D1%8F%20(Group%20Permissions)%20%D1%81%20%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E%20Shibboleth%20%D0%B8%20OpenLDAP.md#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B3%D1%80%D1%83%D0%BF%D0%BF%D0%BE%D0%B2%D1%8B%D1%85-%D1%80%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B9-openldap-%D0%BA-%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%B0%D0%BC-rancher)

Эта страница предоставляет справочную информацию для пользователей Rancher, которые хотят настроить поставщика аутентификации Shibboleth в Rancher.

Поскольку Shibboleth является поставщиком SAML (SAML provider), он не поддерживает поиск групп. Хотя интеграция с Shibboleth может проверять учетные данные пользователя, без дополнительной настройки ее нельзя использовать для назначения разрешений (permission) группам в Rancher.

Одним из решений этой проблемы является настройка поставщика удостоверений OpenLDAP (OpenLDAP identity provider). С помощью бэкенда OpenLDAP для Shibboleth вы сможете выполнять поиск групп в Rancher и назначать их ресурсам (таким как кластеры, проекты или пространства имен) из пользовательского интерфейса Rancher.

# Терминология
- **Shibboleth**: система единого входа для компьютерных сетей и Интернета. С ее помощью люди могут входить в различные системы, используя только одно удостоверение личности. Она проверяет учетные данные пользователя, но сама по себе не обрабатывает членство в группах.
- **SAML**: Язык разметки утверждений безопасности (Security Assertion Markup Language), открытый стандарт для обмена данными аутентификации и авторизации между поставщиком удостоверений (identity provider) и поставщиком услуг (service provider).
- **OpenLDAP**: свободная (free) реализация  протокола Lightweight Directory Access Protocol (LDAP) с открытым исходным кодом. Она используется для управления компьютерами и пользователями организации. Реализация OpenLDAP полезна для Rancher тем, что поддерживает группы. В Rancher можно назначить разрешения (permission) группам, чтобы они могли получать доступ к таким ресурсам, как кластеры, проекты или пространства имен, при условии, что группы уже существуют в поставщике удостоверений (identity provider).
- **IdP** или **IDP**: Поставщик удостоверений (identity provider). OpenLDAP — это пример поставщика удостоверений.

# Добавление групповых разрешений OpenLDAP к ресурсам Rancher
  На приведенной ниже диаграмме показано, как члены группы OpenLDAP могут получать доступ к ресурсам в Rancher, на которые у группы есть разрешения.

Например, владелец кластера может добавить группу OpenLDAP в кластер, чтобы у ее членов появились разрешения на просмотр большинства ресурсов уровня кластера и создание новых проектов. В таком случае члены группы OpenLDAP получат доступ к кластеру, как только они войдут в Rancher.

В этом сценарии OpenLDAP позволяет владельцу кластера выполнять поиск групп при назначении разрешений. Без OpenLDAP не поддерживалась бы функциональность поиска групп.

Когда член группы OpenLDAP входит в Rancher, он перенаправляется в Shibboleth и вводит имя пользователя и пароль.

Shibboleth проверяет эти учетные данные и извлекает атрибуты пользователя из OpenLDAP, в том числе группы. Затем Shibboleth отправляет утверждение SAML (SAML assertion) в Rancher, включая атрибуты пользователя. Rancher использует данные группы, так что пользователь имеет доступ ко всем ресурсам и разрешениям, на которые у групп этого пользователя есть разрешения.

![скриншот](https://user-images.githubusercontent.com/22409457/207049701-bd2d5fb9-6bcc-41de-9ff9-ebf4df037cde.png)



[^1]: [Group Permissions with Shibboleth and OpenLDAP](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/admin-settings/authentication/shibboleth/about/_index.md)
