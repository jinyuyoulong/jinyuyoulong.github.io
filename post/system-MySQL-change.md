---
title: MySQL 数据库迁移
tags:
  - mysql
  - 数据库
id: 534
categories:
  - other technology其他技术
  - PHP
date: 2016-12-15 14:21:18
---

### mac 下迁移数据库的结构和内容

迁移准备：数据库文件（可用工具导出Mysql文件）

##### 注意：由于文件权限的问题 可能不能进入Mysql的data文件内

1.  进入文件 /usr/local/mysql/data
如果打不开，修改文件访问权限，（右击，显示简介，修改文件读写权限）
2.  将相应的文件(如：MYD,MYI,frm) copy进合适的数据库内（文件夹）
3.  打开数据库，查看迁移情况