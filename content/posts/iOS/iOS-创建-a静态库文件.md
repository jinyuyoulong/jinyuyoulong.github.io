---
title: iOS创建.a静态库文件
categories: [iOS]
date: 2016-02-22 16:01:04
tags:
---
步骤：

1.创建项目（选择Framework&Library）

2.删除无用文件，加入希望编译的文件

3.edit scheme &#8211;>release

4.编译真机平台文件：选择ios device

5.编译模拟器平台文件：选择一个模拟器，run运行程序

6.找到编译后的.a文件：选中项目中的.a文件，show in finder

7.将两个文件合并成一个文件：lipo -create 文件路径1 文件路径2 -output 路径3