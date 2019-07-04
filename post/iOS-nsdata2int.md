---
title: NSData转int
id: 55
categories:
  - iOS
date: 2015-04-29 14:03:07
tags:
---

<pre id="best-content-1984648034" accuse="aContent" class="best-text mb-10" style="margin-top: 0px; margin-bottom: 10px; padding: 0px; font-family: arial, &#39;courier new&#39;, courier, 宋体, monospace; white-space: pre-wrap; word-wrap: break-word; color: rgb(51, 51, 51); font-size: 14px; line-height: 24px;">有一种借助string的方法，经验证不对，找了半天终于找到了一个合适的，可是没有看的太明白，特补充记录在此。

1.int&nbsp;-&gt;&nbsp;data
int&nbsp;i&nbsp;=&nbsp;1;
NSData&nbsp;*data&nbsp;=&nbsp;[NSData&nbsp;dataWithBytes:&nbsp;&amp;i&nbsp;length:&nbsp;sizeof(i)];//不多解释，不明白请留言

2.data&nbsp;-&gt;&nbsp;int
int&nbsp;i;
[data&nbsp;getBytes:&nbsp;&amp;i&nbsp;length:&nbsp;sizeof(i)];//必须要事先声明&nbsp;int&nbsp;变量，此处是将data里的数据赋值到&nbsp;int变量&nbsp;i&nbsp;的地址里。</pre>