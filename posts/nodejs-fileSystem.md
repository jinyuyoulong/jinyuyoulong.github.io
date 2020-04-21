---
title: NodeJS 文件系统
categories: [Nodejs]
date: 2016-06-30 11:39:32
---

文件加载顺序：

    st=&gt;start: 开始require
    isfc=&gt;condition: 是否在文件缓冲区
    isnf=&gt;condition: 是否是原生模块
    ff=&gt;operation: 查找文件模块
    lfm=&gt;operation: 根据扩展名载入模块
    cfm=&gt;operation: 缓存文件模块
    isnc=&gt;condition: 是否在原生模块缓存区中
    lnf=&gt;operation: 加载原生模块
    cnf=&gt;operation: 缓存原生模块
    e=&gt;end: 返回exports

    st-&gt;isfc
    isfc(yes)-&gt;e
    isfc(no)-&gt;isnf(no)-&gt;ff-&gt;lfm-&gt;cfm-&gt;e
    isnf(yes)-&gt;isnc(yes)-&gt;lnf-&gt;cnf-&gt;e
    isnc(no)-&gt;e

require方法接受以下几种参数的传递：
http、fs、path等，原生模块。
./mod或../mod，相对路径的文件模块。
/pathtomodule/mod，绝对路径的文件模块。
mod，非原生模块的文件模块。