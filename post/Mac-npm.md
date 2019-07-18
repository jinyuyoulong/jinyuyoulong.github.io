---
title: mac下npm的使用方式
tags:
  - nodejs
  - npm
id: 482
categories:
  - Nodejs
date: 2016-09-08 14:30:11
---

    npm init #创建package.json文件
    npm install xxx -g #全局安装 -g
    npm install xxx #没有package.json文件的时候使用，当前文件下安装
    npm install xxx --save #添加到package.json中的dependencies配置中
    npm install xxx --save-dev #添加到package.json中devDependencies配置中
    npm uninstall xxx 删除包
    npm ls #查看当前目录中已安装的包 -g 全局
    npm update xxx #单包更新
    npm search xxx #搜索
    npm ls xxx 查看xxx包的版本信息
    npm ls --depth 0 #查看安装包列表
    npm prune -x #删除多余的包
    npm ls -g --depth xxx #查看全局npm版本