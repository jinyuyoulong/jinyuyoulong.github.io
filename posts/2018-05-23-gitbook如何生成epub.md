---
title: gitbook如何生成epub
author: fan
type: post
date: 2018-05-23T15:44:43+00:00
url: /gitbook如何生成epub/
categories:
  - Nodejs
  - 工具
tags:
  - gitbook
  - nodejs
format: aside

---
  1. 全局安装gitbook ：npm install -g gitbook
  2. 下载calibre安装应用
  3. 将calibre中的执行文件ebook-convert链接到shall环境：`$ sudo ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin`
  4. 验证ebook-convert可用，terminal下输入ebook-convert 后回车
  5. 如果可用，导出epub文件 gitbook epub ./ ./mbook.epub

node: gitbook 项目需要先 npm install 配置好依赖库,再生成 epub 书籍
  
**Gitbook使用方法** http://www.chengweiyang.cn/gitbook/basic-usage/README.html