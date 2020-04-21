---
title: mac下MongoDB
author: fan
type: post
date: 2016-07-18T10:16:11+00:00
url: /mac下mongodb/
duoshuo_thread_id:
  - 6308606757576901377
  - 6308606757576901377
categories:
  - Nodejs
  - 其他技术
tags:
  - Mongo
  - 数据库

---
### 1. 安装

1.1 解压缩mongo文件，将解压缩后的文件移动到自己喜欢的目录下

### 2. 启动

| bin命令       | 命令解释                               |
| ----------- | ---------------------------------- |
| ./mongod    | 启动mongo服务器                         |
| ./mongo     | 启动mongo客户端，管理数据库                   |
| kill PID -2 | 关闭mongodb服务器（不要使用-9参数，会导致数据库文件损坏）。 |

1.2 由于没有配置环境变量，先测试使用。 终端进入mongodb的安装路径，在bin路径下，执行./mongod启动数据库
  
有可能报错 exception in initAndListen: 29 Data directory /data/db not found
  
这是因为/data/db 目录不存在，若启动时，不指定任何参数， MongoDB 会默认使用 /data/db 目录存储数据，
  
我们可以使用 &#8211;dbpath 来指定其它的路径，比如我使用的是下面这样的命令启动的：
  
`./mongod --dbpath ../data/db`
  
1.3 新开一个终端，在bin路径下执行./mongo启动mongodb管理

### 3. 配置

在mongo文件目录下添加mongo.config
  
编辑内容：

    ##数据文件
    dbpath=/Applications/mongodb/data
    ## 日志文件
    logpath=/Applications/mongodb/log
    

有时候执行./mongo失败，可以执行./mongod

### 4. 使用

`show dbs 显示 数据库s<br />
use dbName 切换数据库<br />
show collections 数据库下的显示表<br />
db.表明.find() 显示表中数据`