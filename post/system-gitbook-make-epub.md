---
title: gitbook如何生成epub
tags:
  - gitbook
url: 736.html
id: 736
categories:
  - Nodejs
  - 工具
date: 2018-05-23 15:44:43
---

1.  全局安装gitbook ：npm install -g gitbook
2.  下载calibre安装应用
3.  将calibre中的执行文件ebook-convert链接到shall环境：$ sudo ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin
4.  验证ebook-convert可用，terminal下输入ebook-convert 后回车
5.  如果可用，导出epub文件 gitbook epub ./ ./mbook.epub

node: gitbook项目需要先npm install,在生成epub