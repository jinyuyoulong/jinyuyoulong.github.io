---
title: thinkphp5开发规范
date: 2018-11-09
---

#### 目录结构

./application

​	./index

​		./controller 控制层

​		./model	模型

​		./view

​	./admin 后台模块

​	command.php 控制台配置，命令行执行，读取该模块

​	common.php 项目的公共文件，通用函数，全局调用

​	config.php 应用的配置文件

​	database.php 数据库配置文件

​	router.php 路由配置文件，对URL进行美化

​	tags.php 应用行为配置文件，默认提供很多钩子，对框架进行扩展，达到无需修改框架源码，注册函数/行为——>改变执行流程

./extend 非composer的第三方库存放地址

./public 网站根目录

​	favicon.ico 网站标签页图标

​	index.php 整个网站入口文件

​	robots.txt 搜索引擎配置文件

​	router.php 快速启动配置文件，无Apache时，通过thinkPHP内置的work server读取该文件，启动框架。例:php -S localhost:8888 router.php 

​	./static 静态资源存放处，例: css、js、image

./runtime	网站运行中缓存文件，日志、缓存、编译文件

./thinkphp	框架文件

​	base.php	定义一些常量

​	composer.json	composer的配置文件

​	console.php 控制台入口文件

​	convention.php 	框架的默认配置文件

​	helper.php	助手函数

​	./lang 	语言包

​	./library	核心

​		./think	框架核心文件

​		./traits	类库扩展

​	LICENSE.txt	法律声明文件

​	logo.png	tp的logo

​	phpunit.xml	phpunit测试的配置文件

​	readme.md	说明文件

​	start.php 框架启动文件

​	./tpl	框架默认模板文件

​		default_index.tpl	控制器模板

​		dispatch_jump.tpl	网站发出成功/失败的跳转模板

​		page_trace.tpl	调试时显示的

​		think_exception.tpl	抛出异常时页面展示的

./vendor	composer安装存放区

#### 开发规范

1. 目录全部小写，下划线分割 例：./application
2. 类库函数名均已.php结尾 例：./application/index/controller 下的 Index.php
3. 类的文件名均已命名空间定义，且命名空间和类库文件所在的路径一致 例：./application/index/controller—— namespace app\index\controller; app定义顶级目录
4. 类文件采用驼峰 首字母大写 其余文件小写+下划线命名
5. 类名与类文件名保持一致，采用驼峰命名&首字母大写
6. 类采用驼峰命名，首字母大写不需要添加后缀  Index √，IndexController ✘
7. 函数名，驼峰，首字母小写 例：public function getUserName(){}
8. 属性名，规则同7
9. 以双下划线__开头的函数或方法为魔术方法
10. 常量和配置 所以的常量都以大写字母+下划线命名 例: define('APP_STATE_','dev');
11. 配置参数以小写字母+下划线命名
12. 其他规范 数据库 表和字段名采用小写+下划线命名，不能以下划线开头 user_name
13. 应用类库名统一使用"app"

