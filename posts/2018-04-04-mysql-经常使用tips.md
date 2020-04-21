---
title: MYSQL 经常使用tips
author: fan
type: post
date: 2018-04-04T09:37:35+00:00
url: /mysql-经常使用tips/
categories:
  - 操作系统
tags:
  - mysql
  - 数据库
format: aside

---
[TOC]

### MySQL三大基础

mysql-devel 开发用到的库以及包含文件
  
mysql mysql 客户端
  
mysql-server 数据库服务器

### 安装

使用yum list mysql_查看了一下我的机子上可用的mysql_安装

##### 安装之后

初始化配置 `sudo mysql_secure_installation`
  
创建新用户：
  
`sudo mysql`
  
`CREATE USER 'sammy'@'localhost' IDENTIFIED BY 'password';`
  
然后，授予新用户合适的权限。例如，授予新用户访问数据库中所有表的权限，及添加、变更和移除用户的权限，通过如下命令即可：
  
`GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;`
  
不需要 `FLUSH PRIVILEGES`只有通过 INSERT, UPDATE或者DELETE命令的方式变更授权表的时候才需要该命令。

### 安装之后设置

设置字符编码
  
/etc/my.cnf 中加入default-character-set=utf8
  
开机启动：
  
添加开机启动：chkconfig &#8211;add mysqld
  
开机启动：chkconfig mysqld on
  
查看开机启动设置是否成功: chkconfig &#8211;list | grep mysql*
  
参考[1]
  
解决phpmyadmin无法登陆，报`The server requested authentication method unknown to the client [caching_sha2_password]`
  
**不要卸载MySQL 8.使用终端程序登录mysql：**
  
`mysql -u root -p`
  
`my_password`
  
`alter user 'username'@'localhost' identified with mysql_native_password by 'password';`
  
**这样就可以了。**

### MYSQL 经常使用tips

  * 启动：brew services start mysql
  * terminal登录：路径 -u 用户名 -p
  * mysql -u root -p 注意必须先启动MySQL
  * 更改初始密码：set password for &#8216;root&#8217;@&#8217;localhost&#8217; = password(&#8216;newPassword&#8217;);

#### db 操作

<pre><code class="language-sh line-numbers">* show databases;
* create database NEW_DB;
* drop database NEW_DB;
* use database DBname;
</code></pre>

#### table 操作

<pre><code class="language-sh line-numbers">* CREATE TABLE table_name (column_name column_type);
* DROP TABLE table_name ;// 删除表
* INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
* SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[OFFSET M ][LIMIT N]
* DELETE FROM table_name [WHERE Clause] // 根据条件删除表内容
* RENAME TABLE
    tbl_name TO new_tbl_name
    [, tbl_name2 TO new_tbl_name2] ...
- show columns from user_info; // 显示表头，列字段
* alter table star_info change SysCreated sys_created int(10) not null default 0 comment '创建时间'; // 更改字段名
</code></pre>

create table example

<pre><code class="language-sh line-numbers">create table user(
id INT(10) not null auto_increment comment '主键ID',
user_name varchar(50) not null comment '用户名',
age tinyint(1) not null default '0' comment '年龄',
email varchar(50) not null comment '邮箱',
pwd varchar(50) not null comment '密码',
primary key (id)
)engine=InnoDB default charset=utf8 comment '用户表';
</code></pre>

数据库与表命名规则：database name/table name/column name 全部小写，单词之间用_ 下划线 分割。因为数据库字段是大小写不敏感的。驼峰命名无意义。

#### 数据类型

##### 数值型

TINYINT 1 字节 (-128，127) (0，255) 小整数值
  
SMALLINT 2 字节 (-32 768，32 767) (0，65 535) 大整数值
  
MEDIUMINT 3 字节 (-8 388 608，8 388 607) (0，16 777 215) 大整数值
  
INT或INTEGER 4 字节 (-2 147 483 648，2 147 483 647) (0，4 294 967 295) 大整数值
  
BIGINT 8 字节 (-9,223,372,036,854,775,808，9 223 372 036 854 775 807) (0，18 446 744 073 709 551 615) 极大整数值
  
FLOAT 4 字节 (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) 0，(1.175 494 351 E-38，3.402 823 466 E+38) 单精度
  
浮点数值
  
DOUBLE 8 字节 (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) 双精度
  
浮点数值
  
DECIMAL 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 依赖于M和D的值 依赖于M和D的值 小数值

##### 日期时间

DATE 3 1000-01-01/9999-12-31 YYYY-MM-DD 日期值
  
TIME 3 &#8216;-838:59:59&#8217;/&#8217;838:59:59&#8217; HH:MM:SS 时间值或持续时间
  
YEAR 1 1901/2155 YYYY 年份值
  
DATETIME 8 1000-01-01 00:00:00/9999-12-31 23:59:59 YYYY-MM-DD HH:MM:SS 混合日期和时间值
  
TIMESTAMP 4
  
1970-01-01 00:00:00/2038
  
结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07，格林尼治时间 2038年1月19日 凌晨 03:14:07
  
YYYYMMDD HHMMSS 混合日期和时间值，时间戳

##### 字符型

CHAR 0-255字节 定长字符串
  
VARCHAR 0-65535 字节 变长字符串
  
TINYBLOB 0-255字节 不超过 255 个字符的二进制字符串
  
TINYTEXT 0-255字节 短文本字符串
  
BLOB 0-65 535字节 二进制形式的长文本数据
  
TEXT 0-65 535字节 长文本数据
  
MEDIUMBLOB 0-16 777 215字节 二进制形式的中等长度文本数据
  
MEDIUMTEXT 0-16 777 215字节 中等长度文本数据
  
LONGBLOB 0-4 294 967 295字节 二进制形式的极大文本数据
  
LONGTEXT 0-4 294 967 295字节 极大文本数据
  
[1]https://www.cnblogs.com/yaomajor/p/5710873.html