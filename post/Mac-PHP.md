---
title: mac 下配置PHP环境
categories: [PHP]
date: 2016-10-20 17:11:54
---

set http.conf
`# ...http_vhost.conf 取消注释#`
`# ServerName www.example.com 打开`

set http.vhost.conf For OSX 10.10 Apache 2.4

设置虚拟机

    &lt;Directory "/Users/username/Sites/"&gt;
    AllowOverride All
    Options Indexes MultiViews FollowSymLinks
    Require all granted
    &lt;/Directory&gt;

set php
LoadModule php5_module libexec/apache2/libphp5.so
修改文件权限 `chmod 777 MetInfo5.3`