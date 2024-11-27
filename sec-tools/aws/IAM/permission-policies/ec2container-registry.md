https://coursehunter.net/course/devsecops-bootcamp?lesson=48
# 1. Permission Policies для EC2 Container Registry (ECR) User

Когда вы создаете IAM пользователя для работы с **Amazon EC2 Container Registry (ECR)**, необходимо настроить специфические права для выполнения операций с контейнерами. Вот пример политики, которая предоставляет доступ к ECR с возможностью управлять образами:

### Пример политики для ECR User

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecr:CreateRepository",
                "ecr:DescribeRepositories",
                "ecr:ListImages",
                "ecr:DescribeImages",
                "ecr:DeleteRepository",
                "ecr:PutImage",
                "ecr:BatchDeleteImage",
                "ecr:GetAuthorizationToken"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ecr:BatchGetImage",
                "ecr:GetDownloadUrlForLayer"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        }
    ]
}
```

### Объяснение политик

- **ecr:CreateRepository**: Позволяет создавать новые репозитории в ECR.
- **ecr:DescribeRepositories**: Позволяет просматривать существующие репозитории и их свойства.
- **ecr:ListImages**: Позволяет просматривать список образов в репозитории.
- **ecr:DescribeImages**: Позволяет просматривать метаданные образов.
- **ecr:DeleteRepository**: Позволяет удалять репозитории.
- **ecr:PutImage**: Позволяет загружать образы в репозиторий.
- **ecr:BatchDeleteImage**: Позволяет удалять образы из репозитория.
- **ecr:GetAuthorizationToken**: Позволяет получить токены авторизации для доступа к ECR.
- **ecr:BatchGetImage** и **ecr:GetDownloadUrlForLayer**: Полномочия для получения образов и слоев из ECR.
- **logs:CreateLogStream** и **logs:PutLogEvents**: Доступ к Amazon CloudWatch Logs для записи логов.

Эта политика предоставит пользователю необходимые разрешения для работы с ECR.

---
