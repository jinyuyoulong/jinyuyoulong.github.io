---
title: Xcode7.3 cannot create __weak reference in file using
author: fan
type: post
date: 2016-04-08T08:26:43+00:00
url: /xcode7-3-cannot-create-__weak-reference-in-file-using/
duoshuo_thread_id:
  - 6278603406965736194
  - 6278603406965736194
categories:
  - iOS

---
升级xcode7.3后项目编译不通过
  
`error：cannot create __weak reference in file using manual reference counting`
  
解决办法：
  
Set Build Settings -> Apple LLVM 7.1 &#8211; Language &#8211; Objective C -> Weak References in Manual Retain Release to YES.