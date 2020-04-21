---
title: swift 常见错误 class xxx has no initializers
author: fan
type: post
date: 2016-04-25T09:09:01+00:00
url: /class-xxx-has-no-initializers/
duoshuo_thread_id:
  - 6278603414574203649
  - 6278603414574203649
categories:
  - swift
tags:
  - iOS
  - swift

---
swift 常见错误
  
error: class xxx has no initializers
  
这是说变量没有初始化，比如
    
var label:UILabel
      
应该写成
      
var label:UILabel?