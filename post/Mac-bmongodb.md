---
title: mac下MongoDB
tags:
  - Mongo
  - 数据库
id: 459
categories:
  - Nodejs
  - other technology其他技术
date: 2016-07-18 18:16:11
---

### 1\. 安装

1.1 解压缩mongo文件，将解压缩后的文件移动到自己喜欢的目录下
1.2 由于没有配置环境变量，先测试使用。 终端进入mongodb的安装路径，在bin路径下，执行./mongod启动数据库

有可能报错 exception in initAndListen: 29 Data directory /data/db not found
这是因为/data/db 目录不存在，若启动时，不指定任何参数， MongoDB 会默认使用 /data/db 目录存储数据，
我们可以使用 --dbpath 来指定其它的路径，比如我使用的是下面这样的命令启动的：
`./mongod --dbpath ../data/db`
新开一个终端，在bin路径下执行./mongo启动mongodb管理

### 2\. 使用

`show dbs 显示 数据库s
use dbName 切换数据库
show collections 数据库下的显示表
db.表明.find() 显示表中数据`