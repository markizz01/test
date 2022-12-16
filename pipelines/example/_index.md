Конвейеры можно настроить либо через пользовательский интерфейс, либо с помощью файла yaml в репозитории, т.е. .rancher-pipeline.yml или .rancher-pipeline.yaml.

В [справочнике по настройке конвейера](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/pipelines/example/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/pipelines/config) мы приводим примеры того, как настроить каждую функцию с помощью пользовательского интерфейса Rancher или конфигурации YAML.
Ниже приведен полный пример rancher-pipeline.yml для тех, кто хочет сразу приступить к делу.

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
        shellScript: echo ${FIRST_KEY} && echo ${ALIAS_ENV}
      # Set environment variables in container for the step
      env:
        FIRST_KEY: VALUE
        SECOND_KEY: VALUE2
      # Set environment variables from project secrets
      envFrom:
      - sourceName: my-secret
        sourceKey: secret-key
        targetKey: ALIAS_ENV
    - runScriptConfig:
        image: busybox
        shellScript: date -R
      # Conditions for steps
      when:
        branch: [ master, dev ]
        event: push
  - name: Publish my image
    steps:
    - publishImageConfig:
        dockerfilePath: ./Dockerfile
        buildContext: .
        tag: rancher/rancher:v2.0.0
        # Optionally push to remote registry
        pushRemote: true
        registry: reg.example.com
  - name: Deploy some workloads
    steps:
    - applyYamlConfig:
        path: ./deployment.yaml
# branch conditions for the pipeline
branch:
  include: [ master, feature/*]
  exclude: [ dev ]
# timeout in minutes
timeout: 30
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
