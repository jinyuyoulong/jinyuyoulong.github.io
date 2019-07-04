---
title: MySQL
date: 2016-10-21 13:27:06
tags:
  - mysql
categories:
  - 数据库
id: 9
---

### MYSQL 经常使用tips
* terminal登录：路径 -u 用户名 -p //mac下 /usr/local/mysql/bin/mysql -u root -p
* 更改初始密码：set password for 'root'@'localhost' = password('newPassword');

#### db 操作
```
* show databases;
* create NEW_DB;
* drop NEW_DB;
* use DBname;
```

#### table 操作
```
* CREATE TABLE table_name (column_name column_type);
* DROP TABLE table_name ;
* INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
* SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[OFFSET M ][LIMIT N]
* DELETE FROM table_name [WHERE Clause]
```
#### brew安装MySQL后的提示

```
==> ./mysql-test-run.pl status --vardir=/tmp/d20171222-28458-qrce7m
mysql的安装地址在这里
==> /usr/local/homebrew/Cellar/mysql/5.7.20/bin/mysqld --initialize-insecure --user=fanjinlong --basedir=/usr/
==> Caveats
我们已经为你安装了 MySQL数据库，有一个没有密码的root账户，如果要设置的话运行：
We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation
MySQL配置的默认只允许从本地连接，连接的换运行命令：mysql -uroot
MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot
启动mysql 重新restart：
To have launchd start mysql now and restart at login:
  brew services start mysql
  或者如果你不想、不需要一个后台服务你可以只运行：
Or, if you don't want/need a background service you can just run:
  mysql.server start
==> Summary

```

创建my.cnf配置文件

1.首先需要知道系统是按如下顺序去找my.cnf：

i.    /etc/my.cnf
ii.   /etc/mysql/my.cnf
iii.  /usr/local/etc/my.cnf
iv.  ~/.my.cnf

2.所以就在/etc下创建my.cnf

$ cd /etc

$ sudo vim my.cnf

配置文件内容如下：

www.mmcaijing.com/2076.html 

#### Navicat 无法连接通过brew 安装的 mysql

提醒一句：如果直接 mysql 是 镜像市场直接下载的 记得配置：

​    MYSQL_ROOT_PASSWORD：你的密码

错误：

Client does not support authentication protocol requested by server; consider upgrading MySQL client

解决方案

1. 先登录：

```
终端执行
mysql -u root -p
#接着输入你的密码
```

2. 解决：

```
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '你的密码';

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';

SELECT plugin FROM mysql.user WHERE User = 'root';
```

 