---
title: app 上架前的打包准备
categories: [iOS]
date: 2015-09-10 15:22:12
tags:
---

<span class="s1">app </span>上架前的打包准备

<span class="s1">1.</span>检查是否是外网环境

2.<span class="s2">更新</span>info.plist<span class="s2">文件版本号</span>

3.product---&gt;scheme----&gt;eidt scheme---&gt;

&nbsp;&nbsp; build configuration 改为 release

4.build setting---&gt;architectures --&gt;&nbsp;

&nbsp;&nbsp; build active architecture only 设置为NO

5.build setting---&gt; code signing --&gt;

&nbsp;&nbsp; Provisioning&nbsp; Profile 设置发布证书

6\. product clean