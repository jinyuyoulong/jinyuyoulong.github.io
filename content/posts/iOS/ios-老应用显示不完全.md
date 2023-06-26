---
title: iOS老应用显示不完全
categories: [iOS]
date: 2016-04-03 13:55:06
---
解决 ：

* 新建launchScreen文件
  
* 设置plist文件，添加Launch screen interface file base name字段 并将value值设为刚刚新建文件的文件名
  
* 删除模拟器或真机上的app重新编译运行