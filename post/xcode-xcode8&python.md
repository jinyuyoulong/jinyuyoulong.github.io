---
title: 使用Xcode8创建Python项目
tags: [Python,xcode]
categories: [Python,工具]
date: 2016-12-06 10:44:31
---

今天想使用一个IDE来开发Python，省的每次写完后都要在terminal上敲命令。选来选去，既然已经安装了Xcode就先用他吧。

### 那么怎么才能使用Xcode创建并运行Python文件呢？

#### 必要准备：mac &amp; Xcode

* * *

#### 开发环境整理：

* * *

##### 1.1 创建

![creat](http://ocnjk5c7r.bkt.clouddn.com/python/python1.1.png)

##### 1.2 选择mac跨平台应用

![select product](http://ocnjk5c7r.bkt.clouddn.com/python/python1.2.png)

##### 1.3 添加项目名称

![add productName](http://ocnjk5c7r.bkt.clouddn.com/python/python1.3.png)

##### 2.1 添加文件

![add file](http://ocnjk5c7r.bkt.clouddn.com/python/python2.1.png)

##### 2.2 Other > Empty

![Other ](http://ocnjk5c7r.bkt.clouddn.com/python/python2.2.png) Empty" />

##### 2.3 给文件命名

![给文件命名](http://ocnjk5c7r.bkt.clouddn.com/python/python2.3.png)
![named](http://ocnjk5c7r.bkt.clouddn.com/python/python2.3.1.png)

##### 3.1 Product > Scheme > Edit Scheme

![Edit Scheme](http://ocnjk5c7r.bkt.clouddn.com/python/python3.1.png)

##### 3.2 Run > info > Executable > Other

![Executable](http://ocnjk5c7r.bkt.clouddn.com/python/python3.2.png)

##### 3.3 Command+Shift+G 定位文件路径Go to the folder:填写/usr/bin/python

![path](http://ocnjk5c7r.bkt.clouddn.com/python/python3.3.png)

##### 3.4 确认选中的可执行文件

![comfirm](http://ocnjk5c7r.bkt.clouddn.com/python/python3.4.png)

##### 3.5 确认Executable 选中python Debug executable 不用选中

![Executable](http://ocnjk5c7r.bkt.clouddn.com/python/python3.5.png)

##### 3.6 Arguments > + >新建的文件名

![Arguments](http://ocnjk5c7r.bkt.clouddn.com/python/python3.6.png)

##### 3.7 Options > Working Directory >项目路径

![Working Directory](http://ocnjk5c7r.bkt.clouddn.com/python/python3.7.png)
选择文件
![select path](http://ocnjk5c7r.bkt.clouddn.com/python/python3.7.1.png)

##### 3.8 确认设置

![comfirm](http://ocnjk5c7r.bkt.clouddn.com/python/python3.8.png)

##### 4 运行

`print "hello world"`
![run](http://ocnjk5c7r.bkt.clouddn.com/python/python4.0.png)