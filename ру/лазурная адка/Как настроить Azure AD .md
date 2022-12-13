





# [Microsoft Graph API](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#microsoft-graph-api-1)

## [Настройка нового пользователя](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#настройка-нового-пользователя)

### [Схема настройки Azure Active Directory](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#схема-настройки-azure-active-directory)

[Зарегистрируйте Rancher в Azure](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#1-зарегистрируйте-rancher-в-azure)

[Создайте новый секрет клиента](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#2-создайте-новый-секрет-клиента)

[Установите необходимые разрешения для Rancher](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#3-установите-необходимые-разрешения-для-rancher)

[Скопируйте данные приложения Azure](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#4-скопируйте-данные-приложения-azure)

[Настройте Azure AD в Rancher](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#5-настройте-azure-ad-в-rancher)

# [Переход с Azure AD Graph API на Microsoft Graph API](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#переход-с-azure-ad-graph-api-на-microsoft-graph-api-1)

### [Обновление конечных точек (endpoint) в пользовательском интерфейсе Rancher](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#обновление-конечных-точек-endpoint-в-пользовательском-интерфейсе-rancher-1)

[Air-gapped окружения](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#air-gapped-окружения)

[Откат миграции](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#откат-миграции)

[Глобальные](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#глобальные)

[China](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#china)

# [Azure AD Graph API](https://github.com/markizz01/test/blob/main/ру/лазурная%20адка/Как%20настроить%20Azure%20AD%20.md#azure-ad-graph-api-1)	

*Примечание переводчика: в зависимости от версии Rancher выберите необходимый Вам раздел:*

- [*Rancher v2.6.7+](#3i3olwj7wlaw)*,*
- [*Rancher v2.6.0 - v2.6.6](#6yjjpi3slul3)*.*

***Rancher v2.6.7+***
# Microsoft Graph API
  Microsoft Graph API теперь является потоком (flow), с помощью которого вы будете настраивать Azure AD. Приведенные ниже разделы помогут [новым пользователям](#_lafnezsa6m95) настроить Azure AD с помощью нового экземпляра, а также помогут существующим владельцам приложений Azure [перейти на новый поток (flow)](#_a85pzsg6i75q).

## Настройка нового пользователя
Если у вас есть экземпляр Active Directory (AD), размещенный в Azure, вы можете настроить Rancher так, чтобы ваши пользователи могли входить в систему, используя свои учетные записи AD. Настройка внешней аутентификации с помощью Azure AD требует, чтобы вы поменяли настройки как в Azure, так и в Rancher.

***Предварительные требования:** Экземпляр Azure AD должен быть настроен.*

***Примечания:***

- *При интеграции с Azure AD поддерживаются только логины, инициированные поставщиком сервиса (Service Provider).*
- *Бо́льшая часть этой процедуры выполняется с [портала Microsoft Azure](https://portal.azure.com/).*
### Схема настройки Azure Active Directory
Настройка Rancher, позволяющая вашим пользователям проходить аутентификацию с помощью своих учетных записей Azure AD, включает в себя несколько процедур. Ознакомьтесь с приведенной ниже схемой, прежде чем приступить к работе.

***Подсказка:** Прежде чем вы начнете, мы рекомендуем создать пустой текстовый файл. Вы можете использовать этот файл для копирования значений из Azure, которые позже будете вставлять в Rancher.*

- [1. Зарегистрируйте Rancher в Azure]
- [2. Создайте новый секрет клиента]
- [3. Установите необходимые разрешения для Rancher]
- [4. Скопируйте данные приложения Azure]
- [5. Настройте Azure AD в Rancher]

### 1. Зарегистрируйте Rancher в Azure
  Прежде чем включить Azure AD в Rancher, вы должны зарегистрировать Rancher в Azure.

1. Войдите в [Microsoft Azure](https://portal.azure.com/) как пользователь с разрешениями администратора. На последующих этапах для настройки потребуются права административного доступа.
1. Используйте поиск, чтобы открыть сервис **App registrations** (записи приложений).

![image](https://user-images.githubusercontent.com/119851242/207311568-5ab9ed91-69a3-47b3-a5fa-88642ae77625.png)


1. Нажмите **New registrations** (новые записи) и заполните форму **Create** (создать).

![image](https://user-images.githubusercontent.com/119851242/207311599-14dd13e1-3fb0-4fa7-bbbb-e7fc2751d8f4.png)


1. Введите имя (что-то, похожее на Rancher).
1. Из **Supported account types** (поддерживаемых типов учетных записей) выберите "Accounts in this organizational directory only (AzureADTest only - Single tenant)"[^2]. Это соответствует параметрам регистрации устаревшего приложения.

***Важно:** На обновленном портале Azure, URI перенаправления (redirect URI) являются синонимами URL-адресов ответов. Чтобы использовать Azure AD с Rancher, вы должны внести Rancher с Azure в белый список (ранее это делалось с помощью URL-адресов ответов). Следовательно, вы должны обязательно заполнить URI перенаправления URL-адресом вашего сервера Rancher, чтобы указать путь верификации (см. ниже).*

1. В разделе [**Redirect URI**](https://docs.microsoft.com/en-us/azure/active-directory/develop/reply-url) (URI перенаправления)  убедитесь, что в выпадающем списке выбран **Web**, и введите URL вашего сервера Rancher в текстовое поле рядом с выпадающим списком. К этому URL-адресу сервера Rancher следует добавить верификационный путь: <MY\_RANCHER\_URL>/verify-auth-azure.

***Совет:** Вы можете найти свой персонализированный URI перенаправления Azure (URL ответа) в Rancher на странице аутентификации Azure AD (Global View > Authentication > Web).*

1. Нажмите кнопку **Register** (зарегистрировать).

***Важно:** Для вступления в силу этого изменения может потребоваться до пяти минут, поэтому не пугайтесь, если вы не сможете пройти аутентификацию сразу после настройки Azure AD.*
### 2. Создайте новый секрет клиента
На портале Azure создайте секрет клиента. Rancher будет использовать этот ключ для аутентификации в Azure AD.

1. Используйте поиск, чтобы открыть сервисы **App registrations** (записи приложений). Затем откройте запись для Rancher, которую вы создали в последней процедуре.

![image](https://user-images.githubusercontent.com/119851242/207311651-93aab6fa-ac90-4d5f-8e35-5c3c8eac3683.png)


1. На панели навигации слева кликните на **Certificates and Secrets** (Сертификаты и секреты).
1. Нажмите **New client secret** (новый секрет клиента).

![image](https://user-images.githubusercontent.com/119851242/207311684-8252d746-98ba-4a13-8d20-7fe8f379d0bc.png)


1. Введите описание (что-то, похожее на Rancher).
1. Выберите срок действия ключа из опций в разделе **Expires** (истекает). В этом раскрывающемся списке указывается дата истечения срока действия ключа. Более короткие сроки действия более безопасны, но требуют от вас создания нового ключа по истечении срока действия.
1. Нажмите **Add** (добавить). Вам не нужно вводить значение — оно будет автоматически заполнено после сохранения.
1. Скопируйте значение ключа и сохраните его в [пустой текстовый файл](#w8jutll22547).

Позже вы введете этот ключ в пользовательский интерфейс Rancher в качестве секрета вашего приложения, **Application Secret**.

Вы не сможете снова получить доступ к значению ключа в пользовательском интерфейсе Azure.
### 3. Установите необходимые разрешения для Rancher
  Затем для Rancher в Azure установите разрешения (permission) API.

***Предупреждение:** Убедитесь, что вы установили разрешения типа Application, а не Delegated. В противном случае вы, возможно, не сможете войти в Azure AD. Эта проблема будет сохраняться даже после отключения/повторного включения Azure AD, и для ее устранения потребуется часовое ожидание или ручное удаление значения кеша.*

1. На панели навигации слева выберите **API permissions** (разрешения API).

![image](https://user-images.githubusercontent.com/119851242/207311714-5355b1e8-11e4-4dd3-84b6-6c61d04f7513.png)


1. Нажмите **Add a permission** (добавить разрешение).
1. В Microsoft Graph выберите следующие Application Permissions (разрешения для приложений):
-   Group.Read.All
-   User.Read.All

![image](https://user-images.githubusercontent.com/119851242/207311772-a3fd1c67-04fc-421e-8c67-e7ad71e9fed1.png)


1. Вернитесь к **API permissions** (разрешения API) в левой панели навигации. Оттуда нажмите **Grant admin consent** (предоставить согласие администратора). Затем нажмите **Yes** (да).

***Примечание:** Примечание: Вы должны войти в систему как администратор Azure, чтобы успешно сохранить настройки разрешений.*
### 4. Скопируйте данные приложения Azure
В качестве последнего шага в Azure, скопируйте данные, которые вы будете использовать, чтобы настроить Rancher для аутентификации с помощью Azure AD, и вставьте их в пустой текстовый файл.

1. Получите свой **Tenant ID** (идентификатор Tenant) для Rancher.
   1. Используйте поиск, чтобы открыть **App registrations** (записи приложений).

![image](https://user-images.githubusercontent.com/119851242/207311827-fa71e957-48a2-43c8-9119-aae917897ad5.png)


1. Найдите запись, которую вы создали для Rancher.
1. Скопируйте **Directory ID** (идентификатор директории) и вставьте его в свой [текстовый файл](#w8jutll22547).

![image](https://user-images.githubusercontent.com/119851242/207311861-ece53eb5-d491-4e9d-9f1b-a748daa824a8.png)


- Вы вставите это значение в Rancher в качестве своего **Tenant ID**.

1. Получите **Application/Client ID** (идентификатор приложения/клиента) от Rancher.
   1. Используйте поиск, чтобы открыть **App registrations** (записи приложения), если это окно еще не открыто.
   1. В разделе **Overview** (обзор) найдите запись, которую вы создали для Rancher.
   1. Скопируйте **Application/Client ID** (идентификатор приложения/клиента) и вставьте его в свой [текстовый файл](#w8jutll22547).

![image](https://user-images.githubusercontent.com/119851242/207312202-a3e5d2e2-ac35-4f43-b51f-f126697c0b65.png)



1. В качестве параметров конечных точек (endpoint) Вы, скорее всего, будете использовать [Standart](#_rb44fnuipudp) и [China](#_7t1l6ayrt9hi). С этими параметрами вам останется только ввести **Tenant ID**, **Application ID** и **Application Secret** (об остальном позаботится Rancher).

![image](https://user-images.githubusercontent.com/119851242/207312231-da9bf7df-6d0b-4bd1-8b5f-88a2cec92ce8.png)


***Для пользовательских конечных точек:***

***Предупреждение:** Пользовательские конечные точки не поддерживаются Rancher и не тестируются им полностью.*

*Вам также нужно будет вручную ввести конечные точки Graph, Token и Auth.*

- *В разделе **App registrations** (записи приложений), нажмите **Endpoints** (конечные точки):*

![image](https://user-images.githubusercontent.com/119851242/207312257-e822f927-d328-4e2b-a6c0-d1013d12885d.png)


- Скопируйте следующие конечные точки в буфер обмена и вставьте их в свой [текстовый файл](#w8jutll22547) (эти значения будут значениями ваших конечных точек в Rancher). Убедитесь, что вы копируете версию v1 этих конечных точек.
  - **Microsoft Graph API endpoint** (конечная точка Graph)
  - **OAuth 2.0 token endpoint (v1)** (конечная точка Token)
  - **OAuth 2.0 authorization endpoint (v1)** (конечная точка Auth)

### 5. Настройте Azure AD в Rancher
  Чтобы завершить настройку, в пользовательском интерфейсе Rancher введите информацию о вашем экземпляре AD, размещенном в Azure.

  Введите значения, которые вы скопировали в свой [текстовый файл](#w8jutll22547).

1. Войдите в Rancher.
1. В левом верхнем углу нажмите **☰> Users & Authentication** (пользователи и аутентификация).
1. В левом навигационном меню выберите **Auth Provider** (поставщик аутентификации).
1. Нажмите **AzureAD**.
1. Заполните форму **Configure Azure AD Account** (настройка учетной записи Azure AD), используя информацию, которую вы скопировали ранее (см. [Скопируйте данные приложения Azure](#_zdbmppxthgq6)).

The following table maps the values you copied in the Azure portal to the fields in Rancher:


| Rancher Field      | Azure Value                           |

|:-|                 |:-|

| Tenant ID          | Directory ID                          |

| Application ID     | Application ID                        |

| Application Secret | Key Value                             |

| Endpoint           | https://login.microsoftonline.com/    |



\>\*\*For Custom Endpoints:\*\* 

\><br/>

\>The following table maps the custom config values you copied in the Azure portal to the fields in Rancher:

\>

\>| Rancher Field      | Azure Value                           |

\>| ------------------ | ------------------------------------- |

\>| Graph Endpoint     | Microsoft Graph API Endpoint          |

\>| Token Endpoint     | OAuth 2.0 Token Endpoint              |

\>| Auth Endpoint      | OAuth 2.0 Authorization Endpoint      |

\><br/>

\>\*\*Important:\*\* When entering the Graph Endpoint in a custom config, remove the tenant ID from the URL, like below:

\>

\><code>http<span>s://g</span>raph.microsoft.com/<del>abb5adde-bee8-4821-8b03-e63efdc7701c</del></code>

1. Нажмите **Enable** (включить).

**Результат:** Настроена аутентификация с помощью Azure Active Directory.

## Переход с Azure AD Graph API на Microsoft Graph API
  Поскольку [Azure AD Graph API](https://docs.microsoft.com/en-us/graph/migrate-azure-ad-graph-overview) устарел в июне 2022 года и будет удален в конце 2022 года, пользователям следует обновить свое приложение Azure AD, чтобы использовать новый [Microsoft Graph API](https://docs.microsoft.com/en-us/graph/use-the-api) в Rancher.
### Обновление конечных точек (endpoint) в пользовательском интерфейсе Rancher
***Важно:** Администраторы должны создать резервную копию (backup) непосредственно перед тем, как они перейдут к миграции конечной точки на шаге 4 ниже.*

1. Обновите разрешения для вашей регистрации в приложении Azure AD, как описано [здесь](#_r0ssl216lib7). **Это очень важно**.
1. Войдите в Rancher.
1. На домашней странице пользовательского интерфейса Rancher обратите внимание на баннер в верхней части экрана, который рекомендует пользователям обновить свою аутентификацию Azure AD. Нажмите на предоставленную ссылку, чтобы сделать это.

![image](https://user-images.githubusercontent.com/119851242/207312423-70526243-ec0e-4df8-b619-3459b53d2c93.png)


1. Чтобы завершить переход на новый Microsoft Graph API, нажмите **Update Endpoint** (обновить конечную точку).

***Примечание:** Перед запуском обновления убедитесь, что ваше приложение Azure имеет [новый набор разрешений](#_r0ssl216lib7).*

![image](https://user-images.githubusercontent.com/119851242/207312474-363f3ce7-54a9-43d0-8a40-9429bb274112.png)


1. Когда вы получите всплывающее предупреждающее сообщение, нажмите **Update** (обновить).

![image](https://user-images.githubusercontent.com/119851242/207312513-647bf904-8bc2-41b1-a03f-05585d4d778f.png)


1. В [таблицах](#uyb8mlia3xka) ниже приведен полный список изменений конечных точек, которые Rancher выполняет самостоятельно. Администраторам не нужно делать это вручную.

### Air-gapped окружения
  В air-gapped окружениях администраторы должны убедиться, что их конечные точки занесены в [белый список](#skk75zb9micx), поскольку URL-адрес конечной точки Graph меняется.

### Откат миграции
Если вам нужно откатить миграцию, пожалуйста, обратите внимание на следующее:

1. Администраторам рекомендуется использовать надлежащий процесс восстановления, если они хотят откатить миграцию. Пожалуйста, для справки ознакомьтесь с документами по резервному копированию и по восстановлению, а также с примерами.
1. Владельцам приложений Azure, которые хотят изменить секрет приложения (Application Secret), также необходимо будет изменить его в Rancher, поскольку Rancher автоматически не обновляет секрет приложения при его изменении в Azure. Обратите внимание, что в Rancher он хранится в секрете Kubernetes под названием azureadconfig-applicationsecret, который находится в пространстве имен cattle-global-data.
1. **Внимание:** Если администраторы обновятся до версии Rancher v2.6.7 с существующей настройкой Azure AD и решат отключить поставщика авторизации, они не смогут восстановить предыдущую настройку, а также не смогут настроить Azure AD заново, используя старый поток (flow). В таком случае администраторам нужно будет снова зарегистрироваться с помощью нового потока авторизации. В настоящее время Rancher использует новый Graph API, и поэтому пользователям необходимо настроить [соответствующие разрешения на портале Azure](#_r0ssl216lib7).
### Глобальные


|**Поле Rancher**|**Устаревшие конечные точки (endpoint)**|
| :-: | :-: |
|Auth Endpoint|[https://login.microsoftonline.com/{tenantID}/oauth2/authorize](https://login.microsoftonline.com/%7BtenantID%7D/oauth2/authorize) |
|Endpoint|<https://login.microsoftonline.com/> |
|Graph Endpoint|<https://graph.windows.net/> |
|Token Endpoint|[https://login.microsoftonline.com/{tenantID}/oauth2/token](https://login.microsoftonline.com/%7BtenantID%7D/oauth2/token) |



|**Поле Rancher**|**Новые конечные точки (endpoint)**|
| :-: | :-: |
|Auth Endpoint|[https://login.microsoftonline.com/{tenantID}/oauth2/v2.0/authorize](https://login.microsoftonline.com/%7BtenantID%7D/oauth2/v2.0/authorize) |
|Endpoint|<https://login.microsoftonline.com/> |
|Graph Endpoint|<https://graph.microsoft.com> |
|Token Endpoint|[https://login.microsoftonline.com/{tenantID}/oauth2/v2.0/token](https://login.microsoftonline.com/%7BtenantID%7D/oauth2/v2.0/token) |

### China

|**Поле Rancher**|**Устаревшие конечные точки (endpoint)**|
| :-: | :-: |
|Auth Endpoint|[https://login.chinacloudapi.cn/{tenantID}/oauth2/authorize](https://login.chinacloudapi.cn/%7BtenantID%7D/oauth2/authorize) |
|Endpoint|<https://login.chinacloudapi.cn/> |
|Graph Endpoint|<https://graph.chinacloudapi.cn/> |
|Token Endpoint|[https://login.chinacloudapi.cn/{tenantID}/oauth2/token](https://login.chinacloudapi.cn/%7BtenantID%7D/oauth2/token) |



|**Поле Rancher**|**Новые конечные точки (endpoint)**|
| :-: | :-: |
|Auth Endpoint|[https://login.partner.microsoftonline.cn/{tenantID}/oauth2/v2.0/authorize](https://login.partner.microsoftonline.cn/%7BtenantID%7D/oauth2/v2.0/authorize) |
|Endpoint|<https://login.partner.microsoftonline.cn/> |
|Graph Endpoint|<https://microsoftgraph.chinacloudapi.cn> |
|Token Endpoint|[https://login.partner.microsoftonline.cn/{tenantID}/oauth2/v2.0/token](https://login.partner.microsoftonline.cn/%7BtenantID%7D/oauth2/v2.0/token) |


***Rancher v2.6.0 - v2.6.6***
# Azure AD Graph API

***Важное:***

- [*API Azure AD Graph](https://docs.microsoft.com/en-us/graph/migrate-azure-ad-graph-overview) *был признан устаревшим в июне 2022 года и будет удален в конце 2022 года. Мы обновим нашу документацию, чтобы сообщить сообществу, когда он будет удален. Сейчас Rancher использует [Microsoft Graph API](https://docs.microsoft.com/en-us/graph/use-the-api) в качестве нового потока (flow) для настройки Azure AD как внешнего поставщика аутентификации.* 
- *Новым пользователям или пользователям, которые хотят выполнить миграцию, рекомендуется обратиться к инструкциям по новому потоку для [Rancher v2.6.7+](#3i3olwj7wlaw).*
- *Уже существующим пользователям, которые не хотят обновляться до версии v2.6.7+, после того, как API Azure AD Graph будет удален придется либо использовать встроенную систему аутентификации Rancher, либо использовать другую стороннюю систему аутентификации и настроить ее в Rancher. Пожалуйста, ознакомьтесь с документами по аутентификации, чтобы узнать, как настроить другие открытые поставщики аутентификации.*



