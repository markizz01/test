В этом разделе вы узнаете, как настраивать конвейеры.

-	[Типы шагов](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%82%D0%B8%D0%BF%D1%8B-%D1%88%D0%B0%D0%B3%D0%BE%D0%B2)
-	[Тип шага: Запустить скрипт](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%82%D0%B8%D0%BF-%D1%88%D0%B0%D0%B3%D0%B0-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D1%8C-%D1%81%D0%BA%D1%80%D0%B8%D0%BF%D1%82)
-	[Тип шага: сборка и публикация изображений](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%82%D0%B8%D0%BF-%D1%88%D0%B0%D0%B3%D0%B0-%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%B8-%D0%BF%D1%83%D0%B1%D0%BB%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F-%D0%B8%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9)
-	[Тип шага: Публикация шаблона каталога](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%82%D0%B8%D0%BF-%D1%88%D0%B0%D0%B3%D0%B0-publish-catalog-template-%D0%BF%D1%83%D0%B1%D0%BB%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F-%D1%88%D0%B0%D0%B1%D0%BB%D0%BE%D0%BD%D0%B0-%D0%BA%D0%B0%D1%82%D0%B0%D0%BB%D0%BE%D0%B3%D0%B0)
-	[Тип шага: развертывание YAML](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%82%D0%B8%D0%BF-%D1%88%D0%B0%D0%B3%D0%B0-%D1%80%D0%B0%D0%B7%D0%B2%D0%B5%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-yaml)
-	[Тип шага: развертывание каталога приложений](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%82%D0%B8%D0%BF-%D1%88%D0%B0%D0%B3%D0%B0-%D1%80%D0%B0%D0%B7%D0%B2%D0%B5%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BA%D0%B0%D1%82%D0%B0%D0%BB%D0%BE%D0%B3%D0%B0)
- [Уведомления](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%83%D0%B2%D0%B5%D0%B4%D0%BE%D0%BC%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F)
-	[Тайм-ауты]()
-	[Триггеры и правила триггеров](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%82%D1%80%D0%B8%D0%B3%D0%B3%D0%B5%D1%80%D1%8B-%D0%B8-%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%B0-%D1%82%D1%80%D0%B8%D0%B3%D0%B3%D0%B5%D1%80%D0%BE%D0%B2)
-	[Переменные среды](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5-%D1%81%D1%80%D0%B5%D0%B4%D1%8B)
-	[Секреты](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%81%D0%B5%D0%BA%D1%80%D0%B5%D1%82%D1%8B)
-	[Справочник по замене переменных конвейера](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D1%81%D0%BF%D1%80%D0%B0%D0%B2%D0%BE%D1%87%D0%BD%D0%B8%D0%BA-%D0%BF%D0%BE-%D0%B7%D0%B0%D0%BC%D0%B5%D0%BD%D0%B5-%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D1%85-%D0%BA%D0%BE%D0%BD%D0%B2%D0%B5%D0%B9%D0%B5%D1%80%D0%B0)
-	[Глобальные параметры выполнения конвейера](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%B3%D0%BB%D0%BE%D0%B1%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BA%D0%BE%D0%BD%D0%B2%D0%B5%D0%B9%D0%B5%D1%80%D0%B0)
    -   [Квота исполнителя](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BA%D0%B2%D0%BE%D1%82%D0%B0-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8F)
    -	[Квота ресурсов для исполнителей](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BA%D0%B2%D0%BE%D1%82%D0%B0-%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%BE%D0%B2-%D0%B4%D0%BB%D1%8F-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D0%B5%D0%B9)
    -	[Пользовательский СА](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D1%81%D0%BA%D0%B8%D0%B9-ca)
-	[Постоянные данные для компонентов конвейера](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BF%D0%BE%D1%81%D1%82%D0%BE%D1%8F%D0%BD%D0%BD%D1%8B%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-%D0%B4%D0%BB%D1%8F-%D0%BA%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82%D0%BE%D0%B2-%D0%BA%D0%BE%D0%BD%D0%B2%D0%B5%D0%B9%D0%B5%D1%80%D0%B0)
-	[Пример rancher-pipeline.yml](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-rancher-pipelineyml)

# Типы шагов

На каждом этапе вы можете добавить столько шагов, сколько хотите. Когда на одном этапе есть несколько шагов, они выполняются одновременно.

Типы шагов включают в себя:

-	Запустить скрипт
-	Создавайте и публикуйте изображения
-	Публикация шаблона каталога
-	Развернуть YAML
-	Развернуть приложение каталога

## Настройка шагов с помощью пользовательского интерфейса

Если вы не добавили никаких этапов, щелкните **Configure pipeline for this branch (Настроить конвейер для этой ветви)** , чтобы настроить конвейер через пользовательский интерфейс.
1.	Добавьте этапы в выполнение вашего конвейера, нажав **Add Stage (Добавить этап) .**
    1.	Введите **Name (имя)** для каждого этапа конвейера.
    2.	Для каждого этапа вы можете настроить правила триггера , нажав **Show Advanced Options (Показать дополнительные параметры)** . *Примечание: это всегда можно обновить позже.*
2.	Создав этап, начните [добавлять шаги](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/_index.md#step-types) , нажав **Add** в **Step (Добавить шаг) .** Вы можете добавить несколько шагов к каждому этапу.

## Настройка шагов с помощью YAML

Для каждого этапа вы можете добавить несколько шагов. Узнайте больше о каждом [типе шага](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/_index.md#step-types) и дополнительных параметрах, чтобы получить подробную информацию о настройке YAML. Это всего лишь небольшой пример того, как иметь несколько этапов с единственным шагом на каждом этапе.

```
# example
stages:
  - name: Build something
    # Conditions for stages
    when:
      branch: master
      event: [ push, pull_request ]
    # Multiple steps run concurrently
    steps:
      - runScriptConfig:
          image: busybox
          shellScript: date -R
  - name: Publish my image
    steps:
    - publishImageConfig:
        dockerfilePath: ./Dockerfile
        buildContext: .
        tag: rancher/rancher:v2.0.0
        # Optionally push to remote registry
        pushRemote: true
        registry: reg.example.com
```

# Тип шага: Запустить скрипт

Шаг **Run Script** выполняет произвольные команды в рабочей области внутри указанного контейнера. Вы можете использовать его для создания, тестирования и выполнения других действий, используя любые утилиты, предоставляемые базовым образом. Для вашего удобства вы можете использовать переменные для ссылки на метаданные выполнения конвейера. Список доступных переменных [см . в справочнике по подстановке переменных конвейера .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/_index.md#pipeline-variable-substitution-reference)

## Настройка скрипта через пользовательский интерфейс

1.	В раскрывающемся списке **«Step Type (Тип шага )»** выберите **«Run Script (Выполнить сценарий)»** и заполните форму.
2.	Щелкните  **Add (Добавить) .**

## Настройка скрипта с помощью YAML
```
# example
stages:
- name: Build something
  steps:
  - runScriptConfig:
      image: golang
      shellScript: go build
```

# Тип шага: сборка и публикация изображений

Шаг **Build and Publish Image** создает и публикует образ Docker. Для успешного завершения этого процесса требуется файл Dockerfile в репозитории вашего исходного кода.
Параметр публикации образа в незащищенном реестре не отображается в пользовательском интерфейсе, но вы можете указать переменную среды в YAML, которая позволяет небезопасно публиковать образ.

## Настройка создания и публикации изображений с помощью пользовательского интерфейса

1.	В раскрывающемся списке **«Step Type (Тип шага) »** выберите **«Build and Publish (Создать и опубликовать) » .**
2.	Заполните остальную часть формы. Описание каждого поля приведено ниже. Когда вы закончите, нажмите **Add (Добавить ).**

|Поле|	Описание|
|:-|:-|
|Путь Dockerfile|	Относительный путь к Dockerfile в репозитории исходного кода. По умолчанию этот путь — ./Dockerfile, что предполагает, что Dockerfile находится в корневом каталоге. Вы можете установить другие пути в разных случаях использования ( ./path/to/myDockerfileнапример).|
|Имя изображения	|Имя изображения в name:tag формате . Адрес реестра не требуется. Например, чтобы построить example.com/repo/my-image:dev, введите repo/my-image:dev.|
|Отправить изображение в удаленный репозиторий|	Параметр для установки реестра, который публикует созданный образ. Чтобы использовать эту опцию, включите ее и выберите реестр из раскрывающегося списка. Если этот параметр отключен, образ помещается во внутренний реестр.|
|Контекст сборки( показать дополнительные параметры )|	По умолчанию корневой каталог исходного кода ( .). Подробнее см. в документации по команде сборки Docker .|

## Настройка сборки и публикации изображений с помощью YAML

Вы можете использовать специфичные аргументы для Docker daemon и файла build. Они не отображаются в пользовательском интерфейсе, но доступны в конвейерном формате YAML, как показано в примере ниже. Доступные переменные среды включают:

|Имя переменной	|Описание|
|:-|:-|
|PLUGIN_DRY_RUN	|Отключить отправку Docker |
|PLUGIN_DEBUG|	Docker daemon выполняется в режиме отладки|
|PLUGIN_MIRROR	|Зеркало реестра Docker daemon|
|PLUGIN_INSECURE	|Docker daemon разрешает небезопасные реестры|
|PLUGIN_BUILD_ARGS	|Docker build args, список, разделенный запятым|

В этом примере показана переменная среды, используемая
на этапе публикации изображения. Эта переменная позволяет вам
публиковать изображение в небезопасном реестре:

```
# This example shows an environment variable being used
# in the Publish Image step. This variable allows you to
# publish an image to an insecure registry:

stages:
- name: Publish Image
  steps:
  - publishImageConfig:
      dockerfilePath: ./Dockerfile
      buildContext: .
      tag: repo/app:v1
      pushRemote: true
      registry: example.com
    env:
      PLUGIN_INSECURE: "true"
      
```

# Тип шага: Publish Catalog Template (Публикация шаблона каталога)

На шаге **« Публикация шаблона каталога »** версия шаблона приложения-каталога (например, чарт Helm) публикуется в репозитории чартов, размещенном на git. Он генерирует коммит git и отправляет его в ваш репозиторий чартов. Для успешного завершения этого процесса требуется папка Чарты в репозитории исходного кода и предварительно настроенный секрет в выделенном пространстве имен конвейера. Любые переменные [в справочнике по подстановке переменных конвейера](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/_index.md#pipeline-variable-substitution-reference) поддерживаются для любого файла в папке чарты.

## Настройка публикации шаблона каталога с помощью пользовательского интерфейса

1.	В раскрывающемся **списке Step Type  (Тип шага)** выберите **Publish Catalog Template  (Опубликовать шаблон каталога) choose Publish Catalog Template .** Заполните остальную часть формы. Описание каждого поля приведено ниже. Когда вы закончите, нажмите **Add (Добавить) .**

|Поле	|Описание|
|:-|:-|
|Папка диаграммы	|Относительный путь к папке диаграммы в репозитории исходного кода, где находится файл Chart.yaml.|
|Название шаблона каталога	|Имя шаблона. Например, wordpress|
|Версия шаблона каталога	|Версия шаблона, которую вы хотите опубликовать, должна соответствовать версии, указанной в файле Chart.yaml.|
|Протокол|	Вы можете выбрать публикацию по протоколу HTTP(S) или SSH.|
|Секрет|	Секрет, в котором хранятся ваши учетные данные Git. Перед добавлением этого шага вам необходимо создать секрет в выделенном пространстве имен конвейера в проекте. Если вы используете протокол HTTP(S), сохраните имя пользователя Git USERNAME и пароль PASSWORD в ключ секрета. Если вы используете протокол SSH, сохраните ключ развертывания Git в  ключе секрета DEPLOY_KEY. После создания секрета выберите его в этой опции.|
|vGit URL-адрес	|URL-адрес Git репозитория чартов, в котором будет опубликован шаблон.|
|Git-ветка	|Ветка Git репозитория чартов, в которой будет опубликован шаблон.|
|Имя автора	|Имя автора, используемое в фиксирующем сообщении.|
|Электронная почта автора	|Электронная почта автора, используемая в фиксирующем сообщении.|

## Настройка публикации шаблона каталога с помощью YAML

Вы можете добавить шаги **публикации шаблона каталога** .rancher-pipeline.yml прямо в файл.
В разделе steps добавьте шаг с publishCatalogConfig. Вы предоставите следующую информацию:

-	Путь: относительный путь к папке диаграммы в репозитории исходного кода, где находится файл Chart.yaml.
-	CatalogTemplate: имя шаблона.
-	Версия: версия шаблона, который вы хотите опубликовать, она должна соответствовать версии, указанной в файле Chart.yaml.
-	GitUrl: URL-адрес git репозитория чартов, в котором будет опубликован шаблон.
-	GitBranch: ветка git репозитория чартов, в которой будет опубликован шаблон.
-	GitAuthor: имя автора, используемое в фиксирующем сообщении.
-	GitEmail: электронная почта автора, используемая в фиксирующем сообщении.
-	Учетные данные: вы должны предоставить учетные данные Git, сославшись на секреты в выделенном пространстве имен конвейера. Если вы публикуете через протокол SSH, введите в ключ развертывания DEPLOY_KEY  переменную среды. Если вы публикуете по протоколу HTTP(S), введите свое имя пользователя и пароль в переменные среды USERNAME и PASSWORD # example

```
stages:
- name: Publish Wordpress Template
  steps:
  - publishCatalogConfig:
      path: ./charts/wordpress/latest
      catalogTemplate: wordpress
      version: ${CICD_GIT_TAG}
      gitUrl: git@github.com:myrepo/charts.git
      gitBranch: master
      gitAuthor: example-user
      gitEmail: user@example.com
    envFrom:
    - sourceName: publish-keys
      sourceKey: DEPLOY_KEY
      
```

# Тип шага: развертывание YAML

На этом шаге в проекте развертываются произвольные ресурсы Kubernetes. Для этого развертывания требуется, чтобы файл манифеста Kubernetes присутствовал в репозитории исходного кода. Подстановка переменных конвейера поддерживается в файле манифеста. Вы можете просмотреть пример файла на [[GitHub.](https://github.com/rancher/pipeline-example-go/blob/master/deployment.yaml)
Список доступных переменных [см . в справочнике по подстановке переменных конвейера .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/_index.md#pipeline-variable-substitution-reference)

## Настройка развертывания YAML с помощью пользовательского интерфейса

1.	В раскрывающемся списке **« Step Type(Тип шага) »** выберите **« Deploy YAML(Развернуть YAML) »** и заполните форму.
2.	Введите **YAML Path**, который является путем к файлу манифеста в исходном коде.
3.	Щелкните **Add.(Добавить) .**


## Настройка развертывания YAML с помощью YAML

```
# example
stages:
- name: Deploy
  steps:
  - applyYamlConfig:
      path: ./deployment.yaml
```

# Тип шага: развертывание приложения-каталога

Шаг **« Deploy Catalog App (Развертывание приложения-каталога) »** развертывает приложение-каталог в проекте. Он установит новое приложение, если его нет, или обновит существующее.

# Настройка развертывания приложения-каталога с помощью пользовательского интерфейса

1.	В раскрывающемся списке **«Step Type (Тип шага) »** выберите **«Deploy Catalog App (Развернуть приложение-каталог) » .**
2.	Заполните остальную часть формы. Описание каждого поля приведено ниже. Когда вы закончите, нажмите **Add(Добавить) .**


|Поле	|Описание|
|:-|:-|
|Каталог	|Каталог, из которого будет использоваться шаблон приложения |
|Имя Шаблона	|Имя шаблона приложения. Например, wordpress.|
|Версия шаблона|	Версия шаблона приложения, которую вы хотите развернуть.|
|Пространство имен	|Целевое пространство имен, в котором вы хотите развернуть приложение |
|Имя приложения	|Имя приложения, которое вы хотите развернуть.|
|Ответы	|Пары ответов "ключ-значение", используемые для развертывания приложения.|

## Настройка развертывания приложения-каталога с помощью YAML

Вы можете добавить шаги **развертывания приложения-каталога** прямо в  файл .rancher-pipeline.yml.
В разделе steps добавьте шаг с applyAppConfig. Вы предоставите следующую информацию:

-	CatalogTemplate:  ID шаблона. Это можно найти, нажав Launch app и выбрав приложение View details. Это последняя часть URL.
-	Версия: версия шаблона, который вы хотите развернуть.
-	Ответы: пары ответов "ключ-значение", используемые для развертывания приложения.
-	Имя: имя приложения, которое вы хотите развернуть.
-	TargetNamespace: целевое пространство имен, в котором вы хотите развернуть приложение.

```
# example
stages:
- name: Deploy App
  steps:
  - applyAppConfig:
      catalogTemplate: cattle-global-data:library-mysql
      version: 0.3.8
      answers:
        persistence.enabled: "false"
      name: testmysql
      targetNamespace: test
      
```

## Время ожидания (Timeout)

По умолчанию каждое выполнение конвейера имеет интервал 60 минут. Если выполнение конвейера не может завершиться в течение времени ожидания, конвейер прерывается.
Настройка времени ожидания с помощью пользовательского интерфейса
Введите новое значение в поле **Timeout (Время ожидания/интервал) .**
Настройка времени ожидания с помощью YAML
В  разделе timeout введите значение времени ожидания в минутах.

```
# example
stages:
  - name: Build something
    steps:
    - runScriptConfig:
        image: busybox
        shellScript: ls
# timeout in minutes
timeout: 30

```

# Уведомления

Вы можете включить уведомления для любых уведомителей в зависимости от состояния сборки конвейера. Прежде чем включать уведомления, Rancher рекомендует настроить уведомители, чтобы можно было сразу добавить получателей.

## Настройка уведомлений через пользовательский интерфейс

1.	В разделе **« Notification (Уведомление) »** включите уведомления, нажав **«Enable (Включить) » .**
2.	Выберите условия для уведомления. Вы можете выбрать получение уведомлений для следующих статусов: Failed, Success, Changed. Например, если вы хотите получать уведомления в случае сбоя выполнения, выберите **Failed(отклонено).**
3.	Если у вас нет существующих уведомителей, Rancher выдаст предупреждение о том, что уведомители не настроены, и предоставит ссылку для перехода на страницу уведомителей. Следуйте [инструкциям](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.0-v2.4/en/cluster-admin/tools/notifiers) , чтобы добавить уведомителя. Если у вас уже есть уведомители, вы можете добавить их в уведомление, нажав кнопку **« Add Recipient (Добавить получателя) » .**
***Примечание.** Уведомители настраиваются на уровне кластера и требуют другого уровня разрешений.*
4.	Для каждого получателя выберите тип уведомления из раскрывающегося списка. В зависимости от типа уведомителя вы можете использовать получателя по умолчанию или заменить получателя другим. Например, если у вас есть уведомитель для Slack , вы можете указать, на какой канал отправлять уведомления. Вы можете добавить дополнительных уведомителей, нажав **Add Recipient (Добавить получателя).**


## Настройка уведомлений с помощью YAML

В разделе notification вы предоставляете следующую информацию:
-	**Получатели(Recipients):** это будет список уведомителей/получателей, которые получат уведомление.
    -	**Уведомитель(Notifier):** идентификатор уведомителя. Это можно найти, найдя уведомитель и выбрав **« View in API(Просмотр в API )»**, чтобы получить идентификатор ID.
    -	**Получатель(Recipient):** в зависимости от типа уведомителя можно использовать «получателя по умолчанию» или переопределить его, указав другого получателя. Например, при настройке Slack Notifier вы выбираете канал в качестве получателя по умолчанию, но если вы хотите отправлять уведомления на другой канал, вы можете выбрать другого получателя.
-	**Условие(Condition):** выберите, при каких условиях вы хотите, чтобы уведомление было отправлено.
-	**Сообщение(Message) (опционально):** если вы хотите изменить сообщение уведомления по умолчанию, вы можете отредактировать его в файле yaml. Примечание. Этот параметр недоступен в пользовательском интерфейсе.

```
# Example
stages:
  - name: Build something
    steps:
    - runScriptConfig:
        image: busybox
        shellScript: ls
notification:
  recipients:
  - # Recipient
    recipient: "#mychannel"
    # ID of Notifier
    notifier: "c-wdcsr:n-c9pg7"
  - recipient: "test@example.com"
    notifier: "c-wdcsr:n-lkrhd"
  # Select which statuses you want the notification to be sent
  condition: ["Failed", "Success", "Changed"]
  # Ability to override the default message (Optional)
  message: "my-message"
  
```

# Триггеры и правила триггеров

После настройки конвейера вы можете активировать его различными способами:

-	**Вручную:**
После настройки конвейера вы можете инициировать сборку, используя последнее определение CI из пользовательского интерфейса Rancher. Когда запускается выполнение конвейера, Rancher динамически выделяет модуль Kubernetes для выполнения ваших задач непрерывной интеграции, а затем удаляет его по завершении.
-	**Автоматически:**
Когда вы включаете репозиторий для конвейера, веб-перехватчики автоматически добавляются в систему контроля версий. Когда пользователи проекта взаимодействуют с репозиторием, отправляя код, открывая пул запросов или создавая тег,  система контроля версий отправляет webhook (веб-перехватчик) на сервер Rancher, запуская выполнение конвейера.
Чтобы использовать эту автоматизацию, для репозитория требуется разрешение на управление webhook (веб-перехватчиком). Поэтому, когда пользователи аутентифицируются и извлекают свои репозитории, будут показаны только те, для которых у них есть разрешение на управление webhook(веб-перехватчиками).

Триггерные правила могут быть созданы для детального управления выполнением конвейера в конфигурации конвейера. Триггерные правила бывают двух типов:

-	**Выполнять это, когда(Run this when):** этот тип правила запускает конвейер, этап или шаг, когда явно срабатывает триггер.
-	**Не запускать это, когда(Do Not Run this when):** правило этого типа пропускает конвейер, стадию или шаг при явном срабатывании триггера.


Если все условия оцениваются как true, то выполняется конвейер/стадия/шаг. В противном случае он пропускается. Когда конвейер пропускается, ни один из конвейеров не выполняется. Когда этап/шаг пропущен, он считается успешным, и последующие этапы/шаги продолжают выполняться.
Расширение символа подстановки ("*") поддерживается в условиях branch .

В этом разделе рассматриваются следующие темы:
-	[Настройка триггеров конвейера](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%BE%D0%B2%D1%82%D1%80%D0%B8%D0%B3%D0%B3%D0%B5%D1%80%D0%BE%D0%B2-%D0%BA%D0%BE%D0%BD%D0%B2%D0%B5%D0%B9%D0%B5%D1%80%D0%B0)
-	[Настройка триггеров этапа](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D1%82%D1%80%D0%B8%D0%B3%D0%B3%D0%B5%D1%80%D0%BE%D0%B2-%D1%8D%D1%82%D0%B0%D0%BF%D0%BE%D0%B2)
-	[Настройка пошаговых триггеров](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%BF%D0%BE%D1%88%D0%B0%D0%B3%D0%BE%D0%B2%D1%8B%D1%85-%D1%82%D1%80%D0%B8%D0%B3%D0%B3%D0%B5%D1%80%D0%BE%D0%B2)
-	[Настройка триггеров с помощью YAML](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D1%82%D1%80%D0%B8%D0%B3%D0%B3%D0%B5%D1%80%D0%BE%D0%B2-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E-yaml)
	
## Настройка запусков/триггеров конвейера

1.	В левом верхнем углу нажмите **☰ > Cluster Management(Управление кластером ).**
2.	Перейдите в кластер, где вы хотите настроить конвейеры, и нажмите **Explore(Исследовать) .**
3.	В раскрывающемся меню на верхней панели навигации выберите проект, в котором вы хотите настроить конвейеры.
4.	На левой панели навигации нажмите **«Legacy > Project > Pipelines(Существующие > «Проект» > «Конвейеры») .**
5.	В репозитории, для которого вы хотите управлять правилами триггеров, выберите вертикальный **⋮ > Edit Config (Изменить конфигурацию) .**
6.	Нажмите **«  Show Advanced Options (Показать дополнительные параметры)» .**
7.	В разделе **« Trigger Rules (Правила триггера) »** настройте правила для запуска или пропуска конвейера.
        1.	Щелкните **Add Rule (Добавить правило) .** В поле **Value (Значение)** введите имя ветки, запускающей конвейер.
        2.	Необязательно: добавьте дополнительные ветки, запускающие сборку.
8.	Щелкните **Done (Готово) .**


## Настройка триггеров этапов

1.	В левом верхнем углу нажмите **☰ > Cluster Management )Управление кластером) .**
2.	Перейдите в кластер, где вы хотите настроить конвейеры, и нажмите Explore(Исследовать) .
3.	В раскрывающемся меню на верхней панели навигации выберите проект, в котором вы хотите настроить конвейеры.
4.	На левой панели навигации нажмите **«Legacy > Project > Pipelines(Существующие > «Проект» > «Конвейеры») .**
5.	В репозитории, для которого вы хотите управлять правилами триггеров, выберите вертикальный **⋮ > Edit Config (Изменить конфигурацию) .**
6.	Найдите **stage (этап)** , для которого вы хотите управлять правилами запуска, щелкните значок **« Edit Изменить) »** для этого этапа.
7.	Щелкните **Show advanced options (Показать дополнительные параметры) .**
8.	В разделе **«Trigger Rules (Правила триггера )»** настройте правила для запуска или пропуска этапа.
      1.	Щелкните **Add Rule (Добавить правило) .**
      2.	Выберите **Type (Тип )**, который запускает этап, и введите значение.

|Тип|Ценность|
|:-|:-|
|Ветвь (Branch)|Имя ветки, запускающей этап.|
|Событие|Тип события, запускающего этап. Значения: Push, Pull Request,Tag|

9.	Нажмите **Save (Сохранить) .**


## Настройка пошаговых триггеров
1.	В левом верхнем углу нажмите **☰ > Cluster Management (Управление кластером) .**
2.	Перейдите в кластер, где вы хотите настроить конвейеры, и нажмите **Explore (Исследовать) .**
3.	В раскрывающемся меню на верхней панели навигации выберите проект, в котором вы хотите настроить конвейеры.
4.	На левой панели навигации нажмите **Legacy > Project > Pipelines. («существующие» > «Проект» > «Конвейеры») .**
5.	В репозитории, для которого вы хотите управлять правилами триггеров, выберите вертикальный **⋮ > Edit Config (Изменить конфигурацию) .**
6.	Найдите **step (шаг)** , для которого вы хотите управлять правилами запуска, щелкните значок **«Edit (Изменить) »** для этого шага.
7.	Щелкните **Show advanced options (Показать дополнительные параметры) .**
8.	В разделе **«Trigger Rules (Правила триггера) »** настройте правила для запуска или пропуска шага.
      1.	Щелкните **Add Rule (Добавить правило) .**
      2.	Выберите **Type (тип)** , запускающий шаг, и введите значение.


|Тип|Ценность|
|:-|:-|
|Ветвь|Имя ветки, запускающей шаг.|
|Событие|Тип события, запускающего шаг. Значения: Push, Pull Request,Tag|


9.	Нажмите Save (Сохранить) .

## Настройка триггеров с помощью YAML
```
# example
stages:
  - name: Build something
    # Conditions for stages
    when:
      branch: master
      event: [ push, pull_request ]
    # Multiple steps run concurrently
    steps:
    - runScriptConfig:
        image: busybox
        shellScript: date -R
      # Conditions for steps
      when:
        branch: [ master, dev ]
        event: push
# branch conditions for the pipeline
branch:
  include: [ master, feature/*]
  exclude: [ dev ]
```

# Переменные среды

При настройке конвейера определенные [типы шагов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/_index.md#step-types) позволяют использовать переменные среды для настройки сценария шага.
Настройка переменных сред с помощью пользовательского интерфейса

1.	В левом верхнем углу нажмите **☰ > Cluster Management (Управление кластером) .**
2.	Перейдите в кластер, где вы хотите настроить пайплайны, и нажмите **Explore (Исследовать) .**
3.	В раскрывающемся меню на верхней панели навигации выберите проект, в котором вы хотите настроить конвейеры.
4.	На левой панели навигации нажмите **Legacy > Project > Pipelines. («существующие» > «Проект» > «Конвейеры») .**
5.	В конвейере, для которого вы хотите изменить триггеры сборки, выберите **⋮ > Edit Config (Изменить конфигурацию) .**
6.	На одном из этапов найдите **step(шаг)** , для которого вы хотите добавить переменную среды, щелкните значок **«Edit (Изменить) » .**
7.	Щелкните **Show advanced options.(Показать дополнительные параметры) .**
8.	Нажмите **«  Add Variable(Добавить переменную) »** и введите ключ и значение в появившихся полях. При необходимости добавьте больше переменных.
9.	Добавьте свои переменные среды в сценарий или файл.
10.	Нажмите **Save(Сохранить) .**

## Настройка переменной среды с помощью YAML
```
# example
stages:
  - name: Build something
    steps:
    - runScriptConfig:
        image: busybox
        shellScript: echo ${FIRST_KEY} && echo ${SECOND_KEY}
      env:
        FIRST_KEY: VALUE
        SECOND_KEY: VALUE2
```

# Секреты

Если вам нужно использовать конфиденциальную информацию в сценариях конвейера (например, пароль), вы можете передать ее с помощью [секретов](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/k8s-in-rancher/secrets) Kubernetes .
Предпосылка
Создайте секрет в том же проекте, что и ваш конвейер, или прямо в пространстве имен, где выполняются модули сборки конвейера.
Примечание. Внедрение секрета отключено для [событий запроса на извлечение .](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/_index.md#triggers-and-trigger-rules)

## Настройка секретов с помощью пользовательского интерфейса

1.	В левом верхнем углу нажмите **☰ > Управление кластером .**
2.	Перейдите в кластер, где вы хотите настроить конвейеры, и нажмите **Исследовать .**
3.	В раскрывающемся меню на верхней панели навигации выберите проект, в котором вы хотите настроить конвейеры.
4.	На левой панели навигации нажмите **«существующие» > «Проект» > «Конвейеры» .**
5.	В конвейере, для которого вы хотите изменить триггеры сборки, выберите **⋮ > Изменить конфигурацию .**
6.	На одном из этапов найдите этап , для которого вы хотите использовать секрет, щелкните значок **« Изменить » .**
7.	Щелкните **Показать дополнительные параметры .**
8.	Щелкните **Add From Secret(Добавить из секрета)** . Выберите секретный файл, который вы хотите использовать. Затем выберите ключ. При желании вы можете ввести псевдоним для ключа.
9.	Нажмите **Сохранить .**


## Настройка секретов с помощью YAML
```
# example
stages:
  - name: Build something
    steps:
    - runScriptConfig:
        image: busybox
        shellScript: echo ${ALIAS_ENV}
      # environment variables from project secrets
      envFrom:
      - sourceName: my-secret
        sourceKey: secret-key
        targetKey: ALIAS_ENV
```

# Справочник по замене переменных конвейера

Для вашего удобства в сценариях конфигурации конвейера доступны следующие переменные. Во время выполнения конвейера эти переменные заменяются метаданными. Вы можете ссылаться на них в виде ${VAR_NAME}.

|Имя переменной	|Описание|
|:-|:-|
|CICD_GIT_REPO_NAME	|Имя репозитория (организация Github опущена).|
|CICD_GIT_URL	|URL репозитория Git.|
|CICD_GIT_COMMIT	|Выполняется идентификатор коммита Git.|
|CICD_GIT_BRANCH	|Git-ветвь этого события.|
|CICD_GIT_REF	|Git справочная спецификация этого события.|
|CICD_GIT_TAG|	Имя тега Git, установленное для события тега.|
|CICD_EVENT	|Событие, инициировавшее сборку ( push, pull_request или tag).|
|CICD_PIPELINE_ID|	Идентификатор Rancher для конвейера.|
|CICD_EXECUTION_SEQUENCE|	Номер сборки конвейера.|
|CICD_EXECUTION_ID|	Комбинация {CICD_PIPELINE_ID}-{CICD_EXECUTION_SEQUENCE}.|
|CICD_REGISTRY	|Адрес реестра Docker для предыдущего шага публикации образа, доступный в файле манифеста Kubernetes  шага Deploy YAML.|
|CICD_IMAGE|	Имя образа, созданного на предыдущем шаге публикации образа, доступного в файле манифеста Kubernetes  шага Deploy YAML. Он не содержит тег изображения.Пример:https://github.com/rancher/pipeline-example-go/blob/master/deployment.yaml |

# Глобальные параметры выполнения конвейера

После настройки провайдера управления версиями можно глобально настроить несколько параметров выполнения конвейеров в Rancher.

## Изменение настроек конвейера
Предварительное условие: поскольку приложение конвейеров устарело в пользу Fleet, перед использованием конвейеров необходимо включить флаг функции для устаревших функций. Обратите внимание, что конвейеры в Kubernetes 1.21+ больше не поддерживаются.

1.	В левом верхнем углу нажмите **☰ > Global Settings(Глобальные настройки) .**
2.	Нажмите **«Feature Flags(Флажки функций)» .**
3.	Перейдите к флажку legacy функции и нажмите **⋮ >Activate (Активировать) .**


Чтобы изменить эти настройки:
1.	В левом верхнем углу нажмите **☰ > Управление кластером .**
2.	Перейдите в кластер, где вы хотите настроить конвейеры, и нажмите **Исследовать .**
3.	В раскрывающемся меню на верхней панели навигации выберите проект, в котором вы хотите настроить конвейеры.
4.	На левой панели навигации нажмите **«Устаревшие» > «Проект» > «Конвейеры» .**


-	[Квота исполнителя](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BA%D0%B2%D0%BE%D1%82%D0%B0-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8F)
-	[Квота ресурсов для исполнителей](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BA%D0%B2%D0%BE%D1%82%D0%B0-%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%BE%D0%B2-%D0%B4%D0%BB%D1%8F-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D0%B5%D0%B9)
-	[Пользовательский СА](https://github.com/markizz01/test/blob/main/pipelines/config/_index.md#%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D1%81%D0%BA%D0%B8%D0%B9-ca)
	
## Квота исполнителя

Выберите максимальное количество исполнителей конвейера. Квота исполнителя определяет, сколько сборок может выполняться одновременно в проекте. Если количество инициированных сборок превышает квоту, последующие сборки будут стоять в очереди до тех пор, пока не откроется вакансия. По умолчанию квота равна 2. Значение 0 или меньше удаляет предел квоты.

## Квота ресурсов для исполнителей

Настройте вычислительные ресурсы для контейнеров агента Jenkins. Когда запускается выполнение конвейера, модуль сборки динамически подготавливается для выполнения ваших задач непрерывной интеграции. Под капотом модуль сборки состоит из одного контейнера агента Jenkins и одного контейнера для каждого шага конвейера. Вы можете [управлять вычислительными ресурсами](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) для каждого контейнера в модуле.

Отредактируйте , Memory Reservation, Memory Limit, CPU Reservation or CPU Limit (резервирование памяти , лимит памяти , резервирование CPU или лимит CPU), затем нажмите «Update Limit and Reservation (Обновить лимит и резервирование) » .

Чтобы настроить вычислительные ресурсы для конвейерных контейнеров, выполните указанные ниже действия.

В файле можно настроить вычислительные ресурсы для контейнеров этапов конвейера  .rancher-pipeline.yml.

На шаге вы предоставите следующую информацию:
-	**Резервирование CPU ( CpuRequest) :** запрос CPU для контейнера шага конвейера.
-	**Лимит CPU ( CpuLimit) :** предел CPU для контейнера шага конвейера.
-	**Резервирование памяти ( MemoryRequest) :** запрос памяти для контейнера шага конвейера.
-	**Ограничение памяти ( MemoryLimit) :** ограничение памяти для контейнера шага конвейера.

```
# example
stages:
  - name: Build something
    steps:
    - runScriptConfig:
        image: busybox
        shellScript: ls
      cpuRequest: 100m
      cpuLimit: 1
      memoryRequest:100Mi
      memoryLimit: 1Gi
    - publishImageConfig:
        dockerfilePath: ./Dockerfile
        buildContext: .
        tag: repo/app:v1
      cpuRequest: 100m
      cpuLimit: 1
      memoryRequest:100Mi
      memoryLimit: 1Gi
 ```     
      
***Примечание.** Rancher устанавливает вычислительные ресурсы по умолчанию для шагов конвейера, за исключением шагов Build and Publish Images и Run Script. Вы можете переопределить значение по умолчанию, указав вычислительные ресурсы таким же образом.*

## Пользовательский CA
Если вы хотите использовать поставщика управления версиями с сертификатом из пользовательского/внутреннего корня СА, необходимо добавить корневые сертификаты СА как часть конфигурации поставщика управления версиями, чтобы модули сборки конвейера успешно работали.

1.	Щелкните  **Edit (Редактировать) cacerts .**
2.	Вставьте корневые сертификаты СА и нажмите **« Save (Сохранить) cacerts» .**


**Результат:** можно использовать конвейеры и новые поды смогут работать с самоподписанным сертификатом.

# Постоянные данные для компонентов конвейера

Внутренний реестр Docker и рабочие нагрузки Minio по умолчанию используют эфемерные тома. Это хранилище по умолчанию работает «из коробки» и упрощает тестирование, но вы теряете образы сборки и журналы сборки, если происходит сбой узла, на котором работает реестр Docker или Minio. В большинстве случаев это нормально. Если вы хотите, чтобы образы и журналы сборки сохранялись при сбоях узлов, вы можете настроить реестр Docker и Minio для использования постоянных томов.
Подробнее о настройке постоянного хранилища для конвейеров [см. на этой странице.](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/pipelines/storage)

# Пример rancher-pipeline.yml

Пример файла конфигурации конвейера находится на этой странице:   https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/config/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/pipelines/example

