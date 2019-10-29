---
title: ReactNative环境搭建
categories: [iOS]
date: 2016-03-18 13:22:50
---

最近换了macbook，于是又要装node.js，记录一下
系统：OS X Mountain Lion 10.8.3
1/ 下载node.js for mac
    http://nodejs.org

    双击安装，一路next，很简单。
    `</pre>

    2/ 测试是否安装成功
       control + space 打开spotlight，输入“终端”，就打开了终端，类似win下的cmd
       输入 node -v , 回车；
       输入 npm -v , 回车
       若无错，则显示版本号

    3/ 测试运行
        在（Finder > ~username ）目录，新建 helloworld.js

    <pre>`若在Finder左侧栏看不到你的用户名，则打开Finder的偏好设置，勾选你的用户名

    回到主题，helloworld.js 内容：
    `</pre>

    *********code start**********

    var http = require('http');
    http.createServer(function(req, res){
        res.writeHead(200, {'Content-Type': 'text/plain'});
        res.end('Hello Worldn');
    }).listen(8808, '127.0.0.1');
    console.log('Server running at http://127.0.0.1:8808');

    **********code end**********
        运行:  打开“终端”，输入“node helloworld.js” （若在其他目录，则在简介里复制完整位置）
       such as： node /Users/inman/Sites/node/helloworld.js

    <pre>`若无误，则显示 Server running at http://127.0.0.1:8808
    打开safari，输入http://127.0.0.1:8808 ， 显示“Hello World”

    that's it !
        退出进程 ctrl+c

本文出自 “简单记录” 博客，请务必保留此出处http://neikvon.blog.51cto.com/4266757/1155998