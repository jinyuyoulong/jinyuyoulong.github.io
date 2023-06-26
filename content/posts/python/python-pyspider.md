---
title: Python_pyspider
date: 2016-11-02 10:34:41
tags: [ppspider]
categories: [Python]
---

### mac 下pyspider的安装

安装环境：`OS X EI Capitan 版本 10.11.6    Python2.7`

此文章书写原因：`经过简单命令pip install pyspider安装失败后，各种解决问题不胜其烦，问题不断。`

失败原因：`EI Capitan 引入了SIP机制（System Integrity Protection）默认下系统启动SIP系统完整性保护机制，无论是对于硬盘还是运行时的进程 限制对系统目录的写操作`

安装成功命令：`pip install pyspider —user -U (基于用户的权限来安装模块包)`

我最终还是放弃了pyspider的使用，对于一名Python小白来说，花在安装爬虫环境的时间太多了，问题也太多，时间效率很不合算。

现在转而使用了一些简单的库BeautifulSoup和PyQuery，两个都是很优秀的html解析库。

熟悉jQuery语法的人推荐使用PyQuery,PyQuery据说是严格按照jQuery语法实现的一套Python解析库。

其他人可以尝试一下BeautifulSoup，简洁而强大。