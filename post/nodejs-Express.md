---
title: Express
date: 2016-08-17 11:05:24
tags:
  - express
category: Express
id: 5
---
nodejs + express 学习记录

设置入口文件
`app.use(express.static(__dirname + '/public'));`
###use方法
use是express注册中间件的方法，它返回一个函数。

中间件（middleware）就是处理HTTP请求的函数。它最大的特点就是，一个中间件处理完，再传递给下一个中间件。App实例在运行过程中，会调用一系列的中间件。

### set方法用于指定变量的值。
app.set("views", __dirname + "/views")
为系统变量views指定值
app.set("view engine", "jade")