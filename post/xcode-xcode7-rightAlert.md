---
title: Xcode7 如何设置访问某些权限时的alert内容
tags: [plist]
categories: [iOS]
date: 2016-03-07 18:28:25
---

举个栗子:
我想访问用户的照片，第一次时会弹出alert框询问用户是否将该权限开放给APP
这时为了增加用户友好度，我们有必要在询问的时候加一些解释和说明。
那么，如何添加呢？
我们在info.plist文件里面设置
info.plist文件--&gt;添加字段Privacy - Photo Library Usage Description--&gt;填写说明文字
[![photoRightDescription](http://fanjinlong.xyz/wp-content/uploads/2016/03/photoRightDescription-300x16.png)](http://blog-fansrss.rhcloud.com/wp-content/uploads/2016/03/photoRightDescription.png)