---
title: 使用Xcode8创建Python项目
author: fan
type: post
date: 2016-12-06T02:44:31+00:00
url: /使用xcode8创建python项目/
categories:
  - Python
  - 工具
tags:
  - Python
  - xcode

---
今天想使用一个IDE来开发Python，省的每次写完后都要在terminal上敲命令。选来选去，既然已经安装了Xcode就先用他吧。

### 那么怎么才能使用Xcode创建并运行Python文件呢？

#### 必要准备：mac & Xcode

* * *

#### 开发环境整理：

* * *

##### 1.1 创建

![creat][1]

##### 1.2 选择mac跨平台应用

![select product][2]

##### 1.3 添加项目名称

![add productName][3]

##### 2.1 添加文件

![add file][4]

##### 2.2 Other > Empty

<img src="http://ocnjk5c7r.bkt.clouddn.com/python/python2.2.png" alt="Other > Empty&#8221; />

##### 2.3 给文件命名

![给文件命名][5]
  
![named][6]

##### 3.1 Product > Scheme > Edit Scheme

![Edit Scheme][7]

##### 3.2 Run > info > Executable > Other

![Executable][8]

##### 3.3 Command+Shift+G 定位文件路径Go to the folder:填写/usr/bin/python

![path][9]

##### 3.4 确认选中的可执行文件

![comfirm][10]

##### 3.5 确认Executable 选中python Debug executable 不用选中

![Executable][11]

##### 3.6 Arguments > + >新建的文件名

![Arguments][12]

##### 3.7 Options > Working Directory >项目路径

![Working Directory][13]
  
选择文件
  
![select path][14]

##### 3.8 确认设置

![comfirm][15]

##### 4 运行

`print "hello world"`
  
![run][16]

 [1]: http://ocnjk5c7r.bkt.clouddn.com/python/python1.1.png
 [2]: http://ocnjk5c7r.bkt.clouddn.com/python/python1.2.png
 [3]: http://ocnjk5c7r.bkt.clouddn.com/python/python1.3.png
 [4]: http://ocnjk5c7r.bkt.clouddn.com/python/python2.1.png
 [5]: http://ocnjk5c7r.bkt.clouddn.com/python/python2.3.png
 [6]: http://ocnjk5c7r.bkt.clouddn.com/python/python2.3.1.png
 [7]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.1.png
 [8]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.2.png
 [9]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.3.png
 [10]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.4.png
 [11]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.5.png
 [12]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.6.png
 [13]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.7.png
 [14]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.7.1.png
 [15]: http://ocnjk5c7r.bkt.clouddn.com/python/python3.8.png
 [16]: http://ocnjk5c7r.bkt.clouddn.com/python/python4.0.png