---
title: ios copy 和 mutableCopy
categories: [iOS]
date: 2016-01-18 19:39:17
tags:
---

通过copy方法可以创建可变对象或不可变对象的不可变副本，对于不可变副本，其对象的值不可以改变。

通过mutableCopy方法可以创建可变对象或不可变对象的可变副本，对于可变副本其对象是可变的。

当我们要给一个copy一个对象的时候，经常需要使用copy方法，可是copy有两种方法：