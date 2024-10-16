## Semgrep Example:
Semgrep JSON Report
```
Result message: 
Detected user input used to manually construct a SQL string. This is usually bad practice because manual construction could accidentally result in a SQL injection. An attacker could use a SQL injection to steal or modify contents of the database. Instead, use a parameterized query which is available by default in most database engines. Alternatively, consider using an object-relational mapper (ORM) such as Sequelize which will protect your queries.
```
```
Snippet:
models.sequelize.query(`SELECT * FROM Products WHERE ((name LIKE '%${criteria}%' OR description LIKE '%${criteria}%') AND deletedAt IS NULL) ORDER BY name`) // vuln-code-snippet vuln-line unionSqlInjectionChallenge dbSchemaChallenge
```

Сообщение об ошибке из отчета Semgrep указывает на потенциальную уязвимость в коде, связанной с SQL-инъекцией. Рассмотрим детали:

### Значение сообщения

1. **Проблема**: В коде происходит ручное построение SQL-запроса с использованием пользовательского ввода (`criteria`). Это может привести к SQL-инъекции, поскольку злоумышленник может подставить вредоносные данные в запрос, чтобы манипулировать содержимым базы данных (например, украсть или изменить данные).

2. **Рекомендация**: Вместо ручного построения SQL-запросов, рекомендуется использовать параметризованные запросы или ORM (Object-Relational Mapper). Параметризованные запросы помогают избежать SQL-инъекций, поскольку ввод пользователя обрабатывается безопасным образом.

### Что делать?

1. **Использовать параметризованные запросы**: 

   Вместо того чтобы вставлять пользовательский ввод прямо в SQL-запрос, используйте параметры. Например:
   ```javascript
   const query = `SELECT * FROM Products WHERE ((name LIKE ? OR description LIKE ?) AND deletedAt IS NULL) ORDER BY name`;
   const replacements = [`%${criteria}%`, `%${criteria}%`];
   models.sequelize.query(query, {
       replacements: replacements,
       type: models.sequelize.QueryTypes.SELECT
   });
   ```

2. **Использовать ORM**: Рассмотрите возможность использования ORM, такого как Sequelize. ORM обеспечивает более безопасный и удобный способ работы с базой данных. Например, с помощью Sequelize вы можете выполнить запрос следующим образом:
   ```javascript
   const products = await models.Product.findAll({
       where: {
           [Op.or]: [
               { name: { [Op.like]: `%${criteria}%` } },
               { description: { [Op.like]: `%${criteria}%` } }
           ],
           deletedAt: null
       },
       order: [['name', 'ASC']]
   });
   ```

3. **Ревью кода**: Проведите ревью вашего кода, и если это возможно, проанализируйте другие участки кода на предмет схожих уязвимостей.

### Заключение

Если не избежать этой проблемы, ваша база данных может стать уязвимой для атак SQL-инъекций. Следование рекомендациям и использование безопасных методов работы с пользовательским вводом поможет защитить ваше приложение и данные.