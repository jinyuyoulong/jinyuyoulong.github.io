---
title: iris-mvc架构的目录拆解
author: fan
type: post
date: 2019-03-13T07:52:15+00:00
excerpt: |
  ├── bootstrap
  │   └── bootstrapper.go		引导者。全局变量配置，模板、session、web socket、Error page
  ├── conf
  │   └── db.go				数据库配置模型。struct model & 实例
url: /iris-mvc架构的目录拆解/
categories:
  - Go
tags:
  - iris

---
<pre><code class="language-shell line-numbers">├── bootstrap
│   └── bootstrapper.go     引导者。全局变量配置，模板、session、web socket、Error page
├── conf
│   └── db.go               数据库配置模型。struct model & 实例
├── dao
│   └── superstar_dao.go    DAO: data access object.对象数据访问，提供 data 的一系列访问方法
├── datasource
│   └── dbhelper.go             数据引擎。单例，负责数据库连接管理（连接，调度）
├── models
│   └── starinfo.go         data model.xorm-——&gt; 数据库表映射模型
├── services
│   └── superstar_service.go    前端数据获取操作 service
└── web                 前端
    ├── controllers     request——&gt; controller ——&gt; Response / view
    ├── main.go         程序入口文件
    ├── main2.go        分布式多服务器 程序入口文件2
    ├── middleware  中间件
    │   ├── basicauth.go    验证授权管理
    │   └── identity        注册全局变量到 iris.context
    ├── public          静态文件
    ├── routes          路由注册、基础配置
    ├── viewmodels  数据校验、进一步处理，非必须。
    └── views           页面模板。template+layout
</code></pre>