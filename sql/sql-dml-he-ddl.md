# SQL DML 和 DDL

注意：**SQL对大小写不敏感！**

可以把 SQL 分为两个部分：**数据操作语言 \(DML\)** 和 **数据定义语言 \(DDL\)**。

SQL \(结构化查询语言\)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。

**查询**和**更新**指令构成了 SQL 的 DML 部分：

* `SELECT` - 从数据库表中获取数据
* `UPDATE` - 更新数据库表中的数据
* `DELETE` - 从数据库表中删除数据
* `INSERT INTO` - 向数据库表中插入数据

SQL 的数据定义语言 \(DDL\) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

SQL 中最重要的 DDL 语句:

* `CREATE DATABASE` - 创建新数据库
* `ALTER DATABASE` - 修改数据库
* `CREATE TABLE` - 创建新表
* `ALTER TABLE` - 变更（改变）数据库表
* `DROP TABLE` - 删除表
* `CREATE INDEX` - 创建索引（搜索键）
* `DROP INDEX` - 删除索引

## SELECT(选择)

SELECT语句用于从表中选取数据。结果被存储在一个结果表中（称为结果集）

```sql
SELECT columnName FROM tableName

/* 选取所有列 */
SELECT * FROM tableName

/* 选取多个列 */
SELECT LastName,FirstName FROM tableName
```

## DISTINCT

使用`DISTINCT`关键词返回唯一不同的值。

```sql
SELECT DISTINCT Company FROM Orders
```

## WHERE

`WHERE`子句用于规定选择的标准

```sql
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值

/* SQL 使用单引号来环绕文本值（大部分数据库系统也接受双引号）。如果是数值，请不要使用引号。*/
SELECT * FROM Persons WHERE City='Beijing'
```

在WHERE子句中可以使用以下运算符。

| 操作符  | 描述         |
| :------ | :----------- |
| =       | 等于         |
| <>      | 不等于       |
| >       | 大于         |
| <       | 小于         |
| >=      | 大于等于     |
| <=      | 小于等于     |
| BETWEEN | 在某个范围内 |
| LIKE    | 搜索某种模式 |

## AND和OR

`AND` 和 `OR` 可在 `WHERE` 子语句中把两个或多个条件结合起来。

如果第一个条件和第二个条件**都成立**，则 **AND 运算符**显示一条记录。

如果第一个条件和第二个条件中**只要有一个成立**，则 **OR 运算符**显示一条记录。

```sql
SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'

SELECT * FROM Persons WHERE firstname='Thomas' OR lastname='Carter'

/* 使用圆括号来组成复杂的表达式 */
SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='William')
AND LastName='Carter'
```

## ORDER BY

`ORDER BY` 语句用于对结果集进行排序。

ORDER BY 语句默认按照升序对记录进行排序。

```sql
SELECT Company, OrderNumber FROM Orders ORDER BY Company

/* 以字母顺序显示公司名称（Company），并以数字顺序显示顺序号（OrderNumber）*/
SELECT Company, OrderNumber FROM Orders ORDER BY Company, OrderNumber

/* 以逆字母顺序显示公司名称 */
SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC

/* 以逆字母顺序显示公司名称，并以数字顺序显示顺序号 */
SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC, OrderNumber ASC
```

## INSERT INTO(插入)

`INSERT INTO` 语句用于向表格中插入新的行

```sql
INSERT INTO 表名称 VALUES (值1, 值2,....)
/* 也可以指定所要插入数据的列 */
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
```

## UPDATE(修改)

Update 语句用于修改表中的数据。

```sql
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
UPDATE Person SET FirstName='Fred' WHERE LastName='Wilson'
```

## DELETE(删除)

DELETE 语句用于删除表中的行。

```sql
DELETE FROM 表名称 WHERE 列名称 = 值
DELETE FROM Person WHERE LastName='Wilson'

/* 可以在不删除表的情况下删除所有的行。这意味着表的结构、属性和索引都是完整的*/
DELETE FROM table_name
DELETE * FROM table_name
```

## TOP子句

TOP 子句用于规定要返回的记录的数目。

**注释：**并非所有的数据库系统都支持 TOP 子句。

```sql
/* SQL Server */
SELECT TOP number|percent column_name(s)
FROM table_name

SELECT TOP 2 * FROM Persons
SELECT TOP 50 PERCENT * FROM Persons


/* MYSQL */
SELECT column_name(s)
FROM table_name
LIMIT number

/* Oracle */
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number
```

## LIKE

LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern
/* 从Persons表中选取居住在以N开始的城市里的人 */
SELECT * FROM Persons
WHERE City LIKE 'N%'
```

注："%" 可用于定义**通配符**

## NOT

通过使用 NOT 关键字，从 "Persons" 表中选取居住在*不包含* "lon" 的城市里的人

```sql
SELECT * FROM Persons
WHERE City NOT LIKE '%lon%'
```

## 通配符

在搜索数据库中的数据时，SQL 通配符可以替代一个或多个字符。

SQL 通配符必须与 LIKE 运算符一起使用。

在 SQL 中，可使用以下通配符：

| 通配符                     | 描述                       |
| :------------------------- | :------------------------- |
| %                          | 替代一个或多个字符         |
| _                          | 仅替代一个字符             |
| [charlist]                 | 字符列中的任何单一字符     |
| [^charlist]或者[!charlist] | 不在字符列中的任何单一字符 |

## IN

IN 操作符允许在 WHERE 子句中规定多个值。

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...)
/* 从表中选取姓氏为 Adams 和 Carter 的人 */
SELECT * FROM Persons
WHERE LastName IN ('Adams','Carter')
```

## BETWEEN

操作符 BETWEEN ... AND 会选取介于两个值之间的数据范围。这些值可以是数值、文本或者日期。

```sql
SELECT * FROM Persons
WHERE LastName
BETWEEN 'Adams' AND 'Carter'

/* 显示范围之外的人 */
SELECT * FROM Persons
WHERE LastName
NOT BETWEEN 'Adams' AND 'Carter'
```

**重要事项：**不同的数据库对 BETWEEN...AND 操作符的处理方式是有差异的。某些数据库会列出介于 "Adams" 和 "Carter" 之间的人，但不包括 "Adams" 和 "Carter" ；某些数据库会列出介于 "Adams" 和 "Carter" 之间并包括 "Adams" 和 "Carter" 的人；而另一些数据库会列出介于 "Adams" 和 "Carter" 之间的人，包括 "Adams" ，但不包括 "Carter" 。

## ALIAS

可以为列名称和表名称指定别名（Alias）

```sql
SELECT column_name(s)
FROM table_name
AS alias_name

SELECT column_name AS alias_name
FROM table_name

/* 假设有两个表分别是："Persons" 和 "Product_Orders"。分别为它们指定别名 "p" 和 "po"。*/
SELECT po.OrderID, p.LastName, p.FirstName
FROM Persons AS p, Product_Orders AS po
WHERE p.LastName='Adams' AND p.FirstName='John'

SELECT LastName AS Family, FirstName AS Name
FROM Persons
```

## JOIN(未完待续)

 join 用于根据两个或多个表中的列之间的关系，从这些表中查询数据。

## UNION

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

**注释：**默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。

```sql
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2
```

