---
title: 抓包调试工具mitmproxy
author: fan
type: post
date: 2016-12-27T02:39:15+00:00
url: /抓包调试工具mitmproxy/
categories:
  - 工具
tags:
  - 抓包

---
安装：brew install mitmproxy
  
其他安装方式: http://docs.mitmproxy.org/en/latest/install.html
  
启动：mitmproxy -p 8080(监听端口号)
  
设置代理，具体设置方法请自行查找
  
抓取https：用 iPhone 打开 Safari 浏览器并输入 mitm.it，安装信任证书
  
使用：键盘上下移动，Enter 键进入查看详情，按 Tab 键切换顶部导航栏
  
拦截修改 request 和 response：
  
输入 i，然后输入 ~s 再按回车键，这时候就进入了 response 拦截模式。如果输入 ~q 则进入 request 的拦截模式，更多的命令可以输入 ？ 查看。
  
其中橘红色的表示请求正被拦截，这时 Enter 进入后 再按 e 就可以修改 request 或者 response。修改时是用 vim 进行编辑的，修改完成后按 a 将请求放行，如果要放行所有请求输入 A 即可