---
title: Xcode7.3 cannot create __weak reference in file using
id: 391
categories:
  - iOS
date: 2016-04-08 16:26:43
tags:
---

升级xcode7.3后项目编译不通过
`error：cannot create __weak reference in file using manual reference counting`
解决办法：
Set Build Settings -> Apple LLVM 7.1 - Language - Objective C -> Weak References in Manual Retain Release to YES.