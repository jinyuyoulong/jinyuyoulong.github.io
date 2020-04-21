---
title: ssh
author: fan
type: post
date: 2016-02-24T08:02:58+00:00
url: /mac-生成-ssh-keys/
duoshuo_thread_id:
  - 6278603380923302657
  - 6278603380923302657
categories:
  - 操作系统
tags:
  - SSH

---
解释

    Secure Shell（安全外壳协议，简称SSH）是一种加密的网络传输协议，可在不安全的网络中为网络服务提供安全的传输环境[1]。
    SSH通过在网络中创建安全隧道来实现SSH客户端与服务器之间的连接[2]。
    虽然任何网络服务都可以通过SSH实现安全传输，SSH最常见的用途是远程登录系统，人们通常利用SSH来传输命令行界面和远程执行命令。使用频率最高的场合类Unix系统，但是Windows操作系统也能有限度地使用SSH。2015年，微软宣布将在未来的操作系统中提供原生SSH协议支持(摘自wikipedia)
    

生成
  
下面是Mac生成方法：
  
1 ：打开终端 输入 ssh-keygen
  
然后系统提示输入文件保存位置等信息，连续敲三次回车即可，生成的SSH key文件保存在中～/.ssh/id_rsa.pub
  
2 然后用文本编辑工具打开该文件，我用的是vim,所以命令是：
  
vim ~/.ssh/id_rsa.pub\`
  
禁忌
  
同一个网站，多个账户之间 不能共用同一个ssh公钥，这会造成服务器无法判断提交者的身份，所以如果有多个账户在同一个网站的话，还是创建多个ssh证书分别管理比较好。
  
多证书管理
  
生成 指定文件名
  
\`ssh-keygen -t rsa -f ~/.ssh/id\_rsa.name -C &#8220;ssh\_name&#8221;
  
创建配置文件
  
vi ~/.ssh/config

    Host git@github.com:aaa
        HostName git@github.com:aaa
        IdentityFile ~/.ssh/id_rsa.aaa
        User git
        HostName git@github.com:bbb
        IdentityFile ~/.ssh/id_rsa
        User git
    

检测是否配置成功

    //查看当前rsa list
    ssh-add -l
    //如果列表中没有新增的rsa， 添加identifile
    ssh-add ~/.ssh/test_id_rsa
    

注： ssh-add 命令是把专用密钥添加到ssh-agent的高速缓存中。是把指定的私钥添加到 ssh-agent 所管理的一个 session 当中。而 ssh-agent 是一个用于存储私钥的临时性的 session 服务，重启之后，ssh-agent 服务也就重置了，session 会话也就失效了。