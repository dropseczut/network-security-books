# 搭建DVWA漏洞环境

在PHPStudy 8.1.1.3版本中，需要修改源代码，才能方便完成SQL注入攻击。

在`MySQL.php`文件第28行，增加`COLLATE utf8_general_ci`，效果如下：

```php
$create_db = "CREATE DATABASE {$_DVWA[ 'db_database' ]} COLLATE utf8_general_ci;";
```
