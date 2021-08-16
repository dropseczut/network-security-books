# AWD

## 比赛形式

## 流程

## 预留后门利用

权限维持

## 防御

1. 备份网站源代码和数据库。

   网站源代码默认位置在`/var/www/html`，可以使用xftp、scp等工具。

   ```
   # 将/var/www/html打包压缩为code.tar.gz
   tar -czf code.tar.gz /var/www/html
   ```

   

   备份数据库。

   Mysql

   ```
   mysqldump -uusername -ppass dbname > dbname.sql
   ```

   

2. 修改口令，包括SSH、Mysql、后台。

### 后门查杀

不死马

crontab

进程