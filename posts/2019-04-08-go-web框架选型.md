---
title: Go Web框架选型
author: fan
type: post
date: 2019-04-08T03:34:20+00:00
url: /go-web框架选型/
categories:
  - Go
tags:
  - Go

---
[TOC]

### Beego

在某些方面，Beego会让人联想到Python中包罗万象的Django Web框架。它具备各种Web应用程序的通用功能，总共有八个模块，你可以根据需要选择使用。除了大多数Web框架中常见的模型-视图-控制器（model-view-controller，MVC）组件外，它还包括访问数据库的对象关系映射（object-relationship map，ORM）、内置缓存处理程序、会话处理工具、日志记录机制和常用的操作HTTP对象的库。
  
Beego还有一个与Django很相似的地方是它的命令行工具。例如，你可以使用bee从头创建Beego应用或管理现有的应用。

### Gin

Go的第一个Web开发框架是Martini，但这个项目已经停止了维护。然而，其他Go框架如雨后春笋般纷纷涌现，它们使用Martini的基本思想，但是具有更好的性能和更多的功能。
  
Gin就是其中的一个项目。它使用修改过的的httprouter软件包来提高速度，并为很多常见的场景提供处理程序，包括中间件、文件上传、日志、将前端HTML组件绑定到后台的数据结构等等。其稳定版API是1.x版本，所以未来的变更应该不会破坏现有的Gin应用。

### Gorilla

Gorilla的定位是“Web工具箱”，而并非MVC风格的框架。它提供的库可以帮忙解决Web服务编程中各种底层的问题，包括context（在请求期间保存状态）、mux（路由和调度），以及实现HTTP上的安全cookie、会话、websocket和RPC等功能。
  
Gorilla没有提供模板、表单和其他前端部分。你需要自己准备这些部分，你可以在其他框架中使用Gorilla的各个组件，或是在独立组件中集成用Gorilla编写的东西。

### Echo

Echo是另一个小框架，主要面向API。例如，它并没有提供模板系统，所以你可以根据需要使用Go自己的html/template。但是，Echo提供了几种常常用于API的中间件模块，例如基本的认证和密钥身份验证、压缩、代理和日志记录。
  
Echo还提供了大量实用的recipe，其中很多无需大费周折就能实现。例如，如果你想使用Let’s Encrypt来管理HTTPS证书，那么可以设置一种recipe来自动安装这些证书。

### Iris

Iris的创建者称其为“真正属于Go的Express.js”，也就是说，它是JavaScript / Node.js的Web框架的Go语言版，它使用最小设计，绝大部分功能都由插件提供。Iris提供基本的MVC功能，自带对中间件、会话、路由和缓存的支持。
  
以下文档包含很多Iris的示例，包括与React前端的交互，或在Docker / Kubernetes环境中运行的项目：https://iris-go.com/v10/recipe

### Revel

Ruby on Rails为MVC风格的Web框架提供了一个通用模式，许多其他语言都仿照Ruby on Rails实现了自己的框架。Revel的创建者将其视作Rails的灵魂。
  
除了提供基本的MVC，Revel还允许你自由使用其他组件来满足其他需求。你可以使用Go自己的原生html/template包，或自己提供。同样，对于HTTP引擎，你也可以使用Go自己的或第三方提供的。缓存可以在本地的内容中完成，也可以通过Memcached或Redis在后台完成。但是，该框架没有数据库的原生ORM。Revel文档的一个例子（https://revel.github.io/examples/booking.html）中使用了Gorp库，但理论上来说你可以使用任何Go ORM。