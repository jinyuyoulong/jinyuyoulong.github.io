---
title: python venv 虚拟环境使用
tags: [Python]
categories: [Python]
date: 2017-07-04 09:53:23
---

virtualenv就是用来为一个应用创建一套“隔离”的Python运行环境。

Python3.3以上的版本通过venv模块原生支持虚拟环境，可以代替[Python](http://lib.csdn.net/base/python "Python知识库")之前的virtualenv。

该venv模块提供了创建轻量级“虚拟环境”，提供与系统[python](http://lib.csdn.net/base/python "Python知识库")的隔离支持。每一个虚拟环境都有其自己的Python二进制（允许有不同的Python版本创作环境），并且可以拥有自己独立的一套Python包。

需要注意的是，在Python3.3中使用”venv”命令创建的环境不包含”pip”，你需要进行手动安装。在Python3.4中改进了这一个缺陷。

安装 **python -m venv .**

启动 **source venv/bin/activate**

退出 **deactivate**

&nbsp;

&nbsp;

virtualenv是如何创建“独立”的Python运行环境的呢？原理很简单，就是把系统Python复制一份到virtualenv的环境，用命令`source venv/bin/activate`进入一个virtualenv环境时，virtualenv会修改相关环境变量，让命令`python`和`pip`均指向当前的virtualenv环境。