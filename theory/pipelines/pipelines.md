### 1) Для чего нужны DAST, SAST и SCA

- **SAST (Static Application Security Testing)**: Это метод анализа исходного кода приложения на наличие уязвимостей еще до его выполнения. SAST помогает разработчикам выявлять возможные проблемы в безопасности на ранних стадиях разработки, позволяя сократить затраты на их исправление и повысить общую безопасность приложения.

- **DAST (Dynamic Application Security Testing)**: В отличие от SAST, DAST проверяет приложение в реальном времени, исследуя его интерфейсы и взаимодействия. Этот метод тестирования позволяет выявлять уязвимости, которые могут возникнуть только в рабочей среде, и играет важную роль в обеспечении безопасности развернутого приложения.

- **SCA (Software Composition Analysis)**: Этот инструмент анализирует зависимости вашего приложения и библиотеки, используемые в проекте, на наличие известных уязвимостей. SCA помогает разработчикам избежать использования небезопасных библиотек и библиотек с уязвимостями, тем самым снижая риски безопасности.

### 2) Как их использовать в работе/пайплайне

- **SAST**: Включите анализ статического кода в CI/CD пайплайн после этапа сборки, чтобы автоматически проверять код на наличие уязвимостей. Это может быть сделано на основе заданий в GitLab CI/CD.

- **DAST**: Запланируйте запустить DAST-тестирование после развертывания приложения в тестовой или рабочей среде. Это обеспечит проверку уже развернутого приложения на наличие уязвимостей.

- **SCA**: Запускайте SCA-сканирование как часть CI/CD пайплайна, по возможности сразу после тестирования, чтобы обеспечить быстрое выявление уязвимостей в зависимостях.

### 3) Примеры работы в пайплайне

Ниже приведен пример интеграции SAST, DAST и SCA в GitLab CI/CD пайплайн с использованием указанных образов:

```yaml
stages:
  - scan
  - deploy

# SAST
sast:
  stage: scan
  image: getcarrier/sast:latest
  script:
    - echo "Starting SAST scan..."
    - /sast/tools/sast-analyzer --source /path/to/your/code
  artifacts:
    paths:
      - sast-report.json

# DAST
dast:
  stage: scan
  image: getcarrier/dast:latest
  script:
    - echo "Starting DAST scan..."
    - /dast/tools/dast-scanner --target http://your-app-url.com --output dast-report.json
  artifacts:
    paths:
      - dast-report.json

# Альтернативный DAST инструмент 
fortify_dast:
  stage: scan
  image: fortifydocker/scancentral-dast-api:latest
  script:
    - echo "Running Fortify DAST scan..."
    - /fortify/scan --url http://your-app-url.com --out fortify-dast-report.json
  artifacts:
    paths:
      - fortify-dast-report.json

# SCA
sca:
  stage: scan
  image: admpresales/sca:latest
  script:
    - echo "Starting SCA scan..."
    - /sca/tools/scan --path /path/to/your/project --output sca-report.json
  artifacts:
    paths:
      - sca-report.json

# Деплой (пример, как может выглядеть)
deploy:
  stage: deploy
  script:
    - echo "Deploying application..."
    - ./deploy-script.sh
```

### Примечания к примеру:
- Убедитесь, что пути к исходному коду и другим ресурсам корректны.
- В каждом задании указаны команды для запуска сканеров. Помните о необходимости согласования команд со спецификациями используемых вами инструментов.
- Использование `artifacts` позволяет сохранять отчеты о сканировании для дальнейшего анализа.
- Проверьте, что ваши образы и инструменты (например, `getcarrier/sast`, `getcarrier/dast`, и др.) установлены и доступны в вашей CI/CD среде.