---
title: 'Cannot find interface declaration for ''ClassA'', superclass of ''ClassB'''
categories: [iOS]
date: 2015-09-22 11:49:57
tags:
---

这个error 是由于 头文件循环引用的原因，导致的。

只要删除其中一个class的头文件中的＃import引用，就会解决这个问题