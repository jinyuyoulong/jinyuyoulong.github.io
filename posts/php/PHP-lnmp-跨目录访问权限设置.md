---
title: LNMP 跨目录访问权限设置
author: fan
type: post
date: 2019-03-15T01:53:05+00:00
url: /lnmp-跨目录访问权限设置/
categories:
  - PHP
  - 操作系统

---
##### LNMP 跨目录访问权限设置

在 ThinkPHP Laravel Typecho 等框架中网站目录一般是在public下，但是public下的程序要跨目录调用public上级目录下的文件，因为LNMP默认是不允许跨目录访问的，所以都是必须要将防跨目录访问的设置去掉，有时候这些框架类的程序提示500错误也可能是这个问题引起的。
  
那么这个问题怎么解决呢？
  
1.2,1.3,1.4,1.5及以上版本，修改对应虚拟主机的配置文件(/usr/local/nginx/conf/vhost/域名.conf)
  
将include enable-php.conf;替换为include enable-php-pathinfo.conf;
  
lnmp v1.1上，修改对应虚拟主机的配置文件(/usr/local/nginx/conf/vhost/域名.conf)
  
去掉#include pathinfo.conf前面的#，把try_files $uri =404; 前面加上# 注释掉。