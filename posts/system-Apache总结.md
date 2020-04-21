---
title: Apache使用总结
date: 2018-07-02
tags: [Apache,PHP]
---



Apache总结

http.conf配置

开启/关闭目录索引

```
<Directory "D:/Apache/blog.phpha.com"> 

Options Indexes FollowSymLinks # 修改为: Options  FollowSymLinks
#Indexes 的作用就是当该目录下没有 index.html 文件时，就显示目录结构，去掉 Indexes ，Apache 就不会显示该目录的列表了。

AllowOverride None     
Order allow,deny     
Allow from all


 </Directory>

```



