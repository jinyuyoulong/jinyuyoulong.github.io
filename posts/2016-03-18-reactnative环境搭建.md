---
title: ReactNative环境搭建
author: fan
type: post
date: 2016-03-18T05:22:50+00:00
url: /reactnative环境搭建/
duoshuo_thread_id:
  - 6278603395209102082
  - 6278603395209102082
categories:
  - iOS

---
最近换了macbook，于是又要装node.js，记录一下
  
系统：OS X Mountain Lion 10.8.3
  
1/ 下载node.js for mac
      
http://nodejs.org

    双击安装，一路next，很简单。
    

2/ 测试是否安装成功
     
control + space 打开spotlight，输入“终端”，就打开了终端，类似win下的cmd
     
输入 node -v , 回车；
     
输入 npm -v , 回车
     
若无错，则显示版本号
  
3/ 测试运行
      
在（Finder > ~username ）目录，新建 helloworld.js

    若在Finder左侧栏看不到你的用户名，则打开Finder的偏好设置，勾选你的用户名
    回到主题，helloworld.js 内容：
    

\***\***\*\\*\*code start\*\*\***\*****
  
var http = require(&#8216;http&#8217;);
  
http.createServer(function(req, res){
      
res.writeHead(200, {&#8216;Content-Type&#8217;: &#8216;text/plain&#8217;});
      
res.end(&#8216;Hello Worldn&#8217;);
  
}).listen(8808, &#8216;127.0.0.1&#8217;);
  
console.log(&#8216;Server running at http://127.0.0.1:8808&#8217;);
  
\***\****\*\\*\*code end\*\*\***\*****
      
运行: 打开“终端”，输入“node helloworld.js” （若在其他目录，则在简介里复制完整位置）
     
such as： node /Users/inman/Sites/node/helloworld.js

    若无误，则显示 Server running at http://127.0.0.1:8808
    打开safari，输入http://127.0.0.1:8808 ， 显示“Hello World”
    that's it !
        退出进程 ctrl+c
    

本文出自 “简单记录” 博客，请务必保留此出处http://neikvon.blog.51cto.com/4266757/1155998