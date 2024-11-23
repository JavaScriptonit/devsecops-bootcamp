# Автоматизация сканирования Docker-образов в AWS ECR

Amazon Elastic Container Registry (ECR) предоставляет возможность хранить и управлять Docker-образами. В этом гиде мы расскажем, как настроить автоматизированное сканирование образов на уязвимости после их загрузки в ECR, используя AWS Lambda и Amazon EventBridge.

## Шаги по настройке

### 1. Создание ECR-репозитория

1. Залогиньтесь в консоль AWS.
2. Перейдите в раздел **ECR**.
3. Выберите **Repositories** и нажмите **Create repository**.
4. Назовите ваш репозиторий и сохраните его.

### 2. Настройка автоматического сканирования в ECR

При создании репозитория вы можете включить автоматическое сканирование образов:

1. При создании репозитория в настройках выберите **Scan images on push** и активируйте его.
2. После этого ECR будет автоматически сканировать образ на уязвимости при каждом его загрузке.

### 3. Настройка уведомлений с помощью Amazon EventBridge

Для автоматизации процесса сканирования и получения уведомлений о результатах сканирования мы будем использовать Amazon EventBridge и AWS Lambda.

#### 3.1 Создание правила в EventBridge

1. Перейдите в раздел **EventBridge** в консоли AWS.
2. Выберите **Rules** и нажмите **Create rule**.
3. Введите имя и описание для правила.
4. Для **Define pattern** выберите **Event pattern**. Вставьте следующий JSON:

   ```json
   {
     "source": ["aws.ecr"],
     "detail-type": ["ECR Image Scan State Change"],
     "detail": {
       "status": ["COMPLETE"]
     }
   }
   ```

5. Перейдите к **Select targets** и выберите **Lambda function**.
6. Укажите функцию, которая будет обрабатывать события.

#### 3.2 Создание AWS Lambda функции

1. Перейдите в раздел **Lambda** в консоли AWS.
2. Нажмите **Create function** и выберите **Author from scratch**.
3. Укажите имя функции, выберите **Python 3.x** в качестве Runtime.
4. Привяжите роль, которая имеет доступ к ECR.

#### 3.3 Код Lambda функции

Вставьте следующий пример кода в вашу Lambda-функцию для получения результатов сканирования:

```python
import json
import boto3

def lambda_handler(event, context):
    client = boto3.client('ecr')
    
    for record in event['Records']:
        detail = record['detail']
        repository_name = detail['repository-name']
        image_digest = detail['image-digest']
        
        response = client.describe_image_scan_findings(
            repositoryName=repository_name,
            imageId={
                'imageDigest': image_digest
            }
        )
        
        findings = response['imageScanFindings']
        print(f"Scan Findings for {repository_name} ({image_digest}): {json.dumps(findings)}")
        
        # Логика для обработки/findings

    return {
        'statusCode': 200,
        'body': json.dumps('Scan processed')
    }
```

### 4. Тестирование автоматизации 

1. Запушьте новый Docker-образ в ECR и убедитесь, что автоматическое сканирование сработало.
2. Проверьте CloudWatch Logs для вашей Lambda-функции, чтобы увидеть результаты сканирования.

### Заключение

Теперь у вас есть настроенная автоматизация для сканирования Docker-образов в AWS ECR. С помощью AWS Lambda и Amazon EventBridge вы можете получать уведомления о результатах сканирования, что позволяет быстро реагировать на уязвимости.

## Полезные ссылки

- [Документация по Amazon ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)
- [Работа с AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [Настройка Amazon EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)

---
Эта статья должна помочь вам настроить автоматизацию для сканирования образов в AWS ECR. Если у вас есть дополнительные вопросы, не стесняйтесь спрашивать!