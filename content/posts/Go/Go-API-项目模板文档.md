---
title: Go-API 项目模板文档
date: 2019-04-03
categories: [Go]
---



### 项目目录结构规范

```
PROJECT_NAME
├── README.md 	//介绍软件及文档入口
├── bin 				//编译好的二进制文件,执行./build.sh自动生成，该目录也用于程序打包
├── build.sh 		//自动编译的脚本
├── doc 				//该项目的文档
├── pack 				//打包后的程序放在此处
├── pack.sh 		//自动打包的脚本，生成类似xxxx.20170713_14:45:35.tar.gz的文件，放在pack文件下
└── src 				//该项目的源代码
    ├── main 		//项目主函数
    ├── test 		//测试
    ├── app 		//项目代码
    ├── public 	//公共文件/静态文件
    └── vendor 	//存放go的库
        ├── github.com/xxx 	//第三方库
        └── xxx.com/abc 		//公司内部的公共库
```

项目的目录结构尽量做到简明、层次清楚。

```
./app
├── bootstrap		//入口引导文件
├── cache
├── config			//项目配置
├── controller	//request请求处理中心 ——> controller ——> Response / view
├── library			//项目工具库
├── log					//日志 —— 考虑发布目录
├── middleware	//中间件
├── model				//data model.xorm -——> 数据库表映射模型
├── route				//路由管理
├── service			//业务数据获取 service
```

