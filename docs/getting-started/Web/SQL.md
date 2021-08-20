# SQL基础

SQL（Structured Query Language，结构化查询语言）是一门ANSI的标准计算机语言，用来管理关系型数据库。不同数据库管理系统，如MySQL、MSSQL，在语法上有差异。

?> 教程以MySQL数据库为例

## 管理工具

- [HeidiSQL](https://www.heidisql.com/)，免费，图形界面，支持MariaDB，MySQL， Microsoft SQL，PostgreSQL和SQLite。

- [phpMyAdmin](https://www.phpmyadmin.net/)，免费，基于Web的MySQL管理软件。

- mysql，MySQL命令行客户端

  ```bash
  $ mysql -u username -p
  mysql> show databases; //查看数据库
  mysql> use dbname; //选择指定数据库
  mysql> show tables; //查看表
  ```

## 语法

### 函数

| 函数       | 作用           |
| ---------- | -------------- |
| user()     | 当前数据库用户 |
| database() | 当前数据库     |
| version()  | 当前数据库版本 |

### 注释
MySQL支持3种注释风格：
- 从`#`字符到行尾
- 从`-- `序列到行尾。注意，`--`（双短划线）后至少有1个空格或控制字符（如，空格，制表符，换行等等）。该语法与标准的SQL语法有差异。
- `/* 注释内容 */`，该语法允许跨行注释。

示例如下：
```sql
mysql> SELECT 1+1; #这条注释作用域到行尾
mysql> SELECT 1+1; -- 这条注释作用域到行尾
mysql> SELECT 1 /* 这是一条行内注释 */ + 1;
mysql> SELECT 1+
/*
这是一条
多行注释
*/
1;
```

此外，MySQL支持C语言风格注释变体。该语法允许写包含MySQL扩展的代码。

```sql
/*! 特殊的MySQL代码 */
```

这种语法，MySQL会分析并执行注释中的代码，但是其他SQL服务器会忽略。并且，该语法支持添加版本号，只允许大于或等于该版本的MySQL服务器执行。比如，允许MySQL 5.1.10 或更高的版本。

```sql
CREATE TABLE t1(a INT, KEY (a)) /*!50110 KEY_BLOCK_SIZE=1024 */;
```

### 逻辑运算符

- AND

  条件1 AND 条件2，当两个条件都满足时，返回`true`

- OR

  条件1 OR 条件2，当两个条件至少1个满足时，返回`true`

```sql
mysql> SELECT user FROM users WHERE user='admin';
+-------+
| user  |
+-------+
| admin |
+-------+
1 row in set (0.00 sec)

mysql> SELECT user FROM users WHERE user='admin' OR 1=1;
+---------+
| user    |
+---------+
| admin   |
| gordonb |
| 1337    |
| pablo   |
| smithy  |
+---------+
5 rows in set (0.00 sec)

mysql> SELECT user FROM users WHERE user='admin' AND 1=2;
Empty set (0.00 sec)
```

### UNION子句

联合查询语句。

?> 两个查询语句返回字段数须一致

```sql
mysql> SELECT 1,2;
+---+---+
| 1 | 2 |
+---+---+
| 1 | 2 |
+---+---+
1 row in set (0.00 sec)
mysql> SELECT 3,4;
+---+---+
| 3 | 4 |
+---+---+
| 3 | 4 |
+---+---+
1 row in set (0.00 sec)
mysql> SELECT 1,2 UNION SELECT 3,4;
+---+---+
| 1 | 2 |
+---+---+
| 1 | 2 |
| 3 | 4 |
+---+---+
2 rows in set (0.01 sec)
mysql> SELECT 1,2,3 UNION SELECT 3,4;
ERROR 1222 (21000): The used SELECT statements have a different number of columns
```

### ORDER BY子句

对查询结果进行排序。

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```

排序字段*column*可以是序号，如1，2，...，当序号不存在时，会提示错误。根据是否报错，可以判断表的字段个数。如，`ORDER BY 8`结果正常，`ORDER BY 9`报错，判断`users`表有8个字段。

```sql
mysql> SELECT * FROM users ORDER BY 1;
mysql> SELECT * FROM users ORDER BY 8;
mysql> SELECT * FROM users ORDER BY 9;
ERROR 1054 (42S22): Unknown column '9' in 'order clause'
```

### GROUP_CONCAT()

返回一个字符串结果，该结果由分组中的值连接组合而成。

```sql
mysql> SELECT GROUP_CONCAT(user) FROM users;
+---------------------------------+
| GROUP_CONCAT(user)              |
+---------------------------------+
| admin,gordonb,1337,pablo,smithy |
+---------------------------------+
1 row in set (0.00 sec)
```

## 备忘录

### 用户

当前用户，`user()`, `current_user()`, `current_user`, `system_user()`, `session_user()`

```sql
mysql> SELECT user();
+----------------+
| user()         |
+----------------+
| dvwa@localhost |
+----------------+
1 row in set (0.00 sec)

SELECT CONCAT_WS(0x3A, user, password) FROM mysql.user WHERE user = 'root';-- (特权)
```

### 版本

version()、@@version()、@@GLOBAL.VERSION

```sql
mysql> select version();
+-----------+
| version() |
+-----------+
| 5.7.26    |
+-----------+
1 row in set (0.00 sec)
```

### 数据库

```sql
SELECT database();--当前数据库
SELECT schema_name FROM information_schema.schemata;
SELECT DISTINCT(db) FROM mysql.db;--(Privileged)
```

### 表

```sql
mysql> SELECT GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema=database();
+--------------------------+
| GROUP_CONCAT(table_name) |
+--------------------------+
| guestbook,users          |
+--------------------------+
1 row in set (0.00 sec)
```

### 字段

```sql
mysql> SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema=database() AND table_name='users';
+---------------------------------------------------------------------------+
| GROUP_CONCAT(column_name)                                                 |
+---------------------------------------------------------------------------+
| user_id,first_name,last_name,user,password,avatar,last_login,failed_login |
+---------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

### 主机名

```sql
mysql> SELECT @@hostname;
+-----------------+
| @@hostname      |
+-----------------+
| DESKTOP-H4QNVJS |
+-----------------+
1 row in set (0.00 sec)
```

## 参考资料

- 廖雪峰，[SQL教程](https://www.liaoxuefeng.com/wiki/1177760294764384)
