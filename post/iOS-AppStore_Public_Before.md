---
title: App Store上架前的准备
categories: [iOS]
date: 2015-08-21 17:10:11
tags:
---

一、制作ipa发布包

1、所需装备

1）一个distribution发布版证书

2）Xcode，iTunes，完成的项目，这都不用说了

开始配置Xcode

1.  Build Setting ---&gt; code signing ---&gt; Provisioning profile 设为发布证书

2.  Build Setting ---&gt;&nbsp;Architectures ---&gt; build active Architectures Only 设为NO&nbsp;

&nbsp; 3\. &nbsp;Product---&gt;scheme----&gt; edit scheme---&gt;build configration 改为release

然后：shift+command+k clean项目 ---&gt;command+B build新项目

将Xcode里面的项目app拖到iTunes的应用里面，再将项目拖出 ，到文件里面，至此成功，可以准备提交到iTunes connection了。