Цель этой страницы — объяснить общие понятия и терминологию, связанные с конвейерами.

-	**Конвейер:**
Конвейер — это процесс доставки программного обеспечения, который разбит на различные этапы и шаги. Настройка конвейера может помочь разработчикам выпускать новое программное обеспечение максимально быстро и эффективно. В Rancher вы можете настроить конвейеры для каждого из ваших проектов Rancher. Конвейер основан на конкретном репозитории. Он определяет процесс создания, тестирования и развертывания вашего кода. Rancher использует [конвейер в качестве](https://jenkins.io/doc/book/pipeline-as-code/) модели кода. Конфигурация конвейера представлена в виде файла конвейера в репозитории исходного кода с использованием имени файла .rancher-pipeline.yml или .rancher-pipeline.yaml.
-	**Этапы:**
Этап конвейера состоит из нескольких шагов. Этапы выполняются в порядке, указанном в файле конвейера. Шаги этапа выполняются одновременно. Этап начинается, когда все шаги предыдущего этапа завершаются без сбоев.
-	**Шаги:**
Шаг конвейера выполняется внутри указанного этапа. Шаг терпит неудачу, если он завершается с кодом, отличным от 0. Если шаг завершается с этим кодом ошибки, весь конвейер дает сбой и завершается.
-	**Workspace (Рабочее пространство):**
Рабочая область — это рабочий каталог, совместно используемый всеми этапами конвейера. В начале конвейера исходный код извлекается в рабочую область. Команда для каждого шага загружается в рабочую область. Во время выполнения конвейера артефакты с предыдущего шага будут доступны на следующих шагах. Рабочий каталог — это эфемерный том, который будет очищен модулем исполнителя после завершения выполнения конвейера.

Как правило, этапы конвейера включают в себя:

-	**Строить:**
Каждый раз, когда код проверяется в вашем репозитории, конвейер автоматически клонирует репозиторий и создает новую итерацию вашего программного обеспечения. На протяжении всего этого процесса программное обеспечение обычно проверяется с помощью автоматизированных тестов.
-	**Публиковать:**
После завершения сборки создается либо образ Docker, который публикуется в реестре Docker, либо публикуется шаблон каталога.
-	**Развертывать:**
После публикации артефактов вы должны выпустить свое приложение, чтобы пользователи могли начать использовать обновленный продукт.
