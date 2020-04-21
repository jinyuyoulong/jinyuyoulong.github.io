---
title: Xcode7 如何设置访问某些权限时的alert内容
author: fan
type: post
date: 2016-03-07T10:28:25+00:00
url: /xcode7-如何设置访问某些权限时的alert内容/
duoshuo_thread_id:
  - 6278603395053912834
  - 6278603395053912834
categories:
  - iOS
tags:
  - plist

---
举个栗子:
  
我想访问用户的照片，第一次时会弹出alert框询问用户是否将该权限开放给APP
  
这时为了增加用户友好度，我们有必要在询问的时候加一些解释和说明。
  
那么，如何添加呢？
  
我们在info.plist文件里面设置
  
info.plist文件&#8211;>添加字段Privacy &#8211; Photo Library Usage Description&#8211;>填写说明文字
  
<a href="http://blog-fansrss.rhcloud.com/wp-content/uploads/2016/03/photoRightDescription.png" rel="attachment wp-att-345"><img class="alignleft size-medium wp-image-345" src="http://fanjinlong.xyz/wp-content/uploads/2016/03/photoRightDescription-300x16.png" alt="photoRightDescription" width="300" height="16" /></a>