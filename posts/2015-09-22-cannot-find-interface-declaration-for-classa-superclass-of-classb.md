---
title: "Cannot find interface declaration for 'ClassA', superclass of 'ClassB'"
author: fan
type: post
date: 2015-09-22T03:49:57+00:00
url: /cannot-find-interface-declaration-for-classa-superclass-of-classb/
duoshuo_thread_id:
  - 6278603345921852162
  - 6278603345921852162
views:
  - 4
  - 4
categories:
  - iOS

---
这个error 是由于 头文件循环引用的原因，导致的。

只要删除其中一个class的头文件中的＃import引用，就会解决这个问题