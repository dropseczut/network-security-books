# 搭建DVWA漏洞环境

Damn Vulnerable Web Application (DVWA)(译注：可以直译为："该死的"不安全Web应用网站)，是一个编码糟糕的、易受攻击的 PHP/MySQL Web应用程序。 它的主要目的是帮助安全专业人员在合法的环境中，测试他们的技能和工具，帮助 Web 开发人员更好地了解如何增强 Web 应用程序的安全性，并帮助学生和教师在受控的课堂环境中，了解 Web 应用程序的安全。

!> DVWA十分易受攻击！ **不要将其上传到您的云服务器的公共 html 文件夹或任何面向 Internet 的服务器**，因为它们会受到危害。 建议使用虚拟机，设置为NAT组网方式。

## 下载

虽然有各种版本的 DVWA，但唯一受支持的版本是来自官方 GitHub 存储仓库的最新源码。 你可以克隆它：

```bash
git clone https://github.com/digininja/DVWA.git
```

或者 [下载文件的ZIP](https://github.com/digininja/DVWA/archive/master.zip)

## 安装

### Windows + PHPStudy

首先，根据该教程完成WAMP环境的安装。

只需解压缩 dvwa.zip，将解压缩的文件放在您的公共 html 文件夹中，然后使用浏览器访问：`http://127.0.0.1/dvwa/setup.php`

### 数据库配置

复制文件`./config/config.inc.php.dist`为`./configconfig.inc.php`，默认数据库认证信息如下，

```php
$_DVWA[ 'db_server' ]   = '127.0.0.1';
$_DVWA[ 'db_database' ] = 'dvwa';
$_DVWA[ 'db_user' ]     = 'dvwa';
$_DVWA[ 'db_password' ] = 'p@ssw0rd';
$_DVWA[ 'db_port'] = '3306';
```

### PHP配置

- `allow_url_include = on` - 允许远程文件包含 (RFI) [[allow_url_include](https://secure.php.net/manual/en/filesystem.configuration.php#ini.allow-url-include)]
* `allow_url_fopen = on` - 允许远程文件包含 (RFI) [[allow_url_fopen](https://secure.php.net/manual/en/filesystem.configuration.php#ini.allow-url-fopen)]
- `safe_mode = off` - （如果 PHP <= v5.4）允许 SQL 注入（SQLi） [[safe_mode](https://secure.php.net/manual/en/features.safe-mode.php)]
- `magic_quotes_gpc = off` - （如果 PHP <= v5.4）允许 SQL 注入（SQLi） [[magic_quotes_gpc](https://secure.php.net/manual/en/security.magicquotes.php)] 
- `display_errors = off` - （可选）隐藏 PHP 警告消息以使其不那么冗长 [[display_errors](https://secure.php.net/manual/en/errorfunc.configuration.php#ini.display-errors)]

### 文件夹权限

- `./hackable/uploads/` - 需要允许web服务可写（用于文件上传）。

## 错误处理

### Illegal mix of collations for operation ‘UNION’

UNION操作的排序规则不一致。

`information_schema`和`dvwa`的默认排序规则`DEFAULT_COLLATION_NAME `不一致。

```sql
mysql> select * from information_schema.schemata;
+--------------+--------------------+----------------------------+------------------------+----------+
| CATALOG_NAME | SCHEMA_NAME        | DEFAULT_CHARACTER_SET_NAME | DEFAULT_COLLATION_NAME | SQL_PATH |
+--------------+--------------------+----------------------------+------------------------+----------+
| def          | mysql              | utf8                       | utf8_general_ci        |     NULL |
| def          | information_schema | utf8                       | utf8_general_ci        |     NULL |
| def          | performance_schema | utf8mb4                    | utf8mb4_0900_ai_ci     |     NULL |
| def          | sys                | utf8mb4                    | utf8mb4_0900_ai_ci     |     NULL |
| def          | dvwa               | utf8                       | utf8_unicode_ci        |     NULL |
+--------------+--------------------+----------------------------+------------------------+----------+
5 rows in set (0.00 sec)
```

原因是`PHPStudy`的MySQL配置文件`collation-server=utf8_unicode_ci`，DVWA新建的数据库排序规

- 解决方法一，修改DVWA源代码

  修改文件`dvwa/includes/DBMS/MySQL.php`第28行，增加`COLLATE utf8_general_ci`，效果如下：

  ```php
  $create_db = "CREATE DATABASE {$_DVWA[ 'db_database' ]} COLLATE utf8_general_ci;";
  ```
  接下来，在DVWA面板重置数据库即可。

- 解决方法二，修改数据库的`排序规则`设置

  打开phpMyAdmin，左侧选择数据库，点击`操作`选项卡，修改下方`排序规则`为`utf8_general_ci`，并勾选`更改所有表排序规则`和`更改所有表列的排序规则`。

- 解决方法三，对查询结果进行编码

## 参考资料

- [DVWA中文文档](https://github.com/digininja/DVWA/blob/master/README.zh.md)

