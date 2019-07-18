---
title: ViewController 界面的推出调用时间
id: 229
categories:
  - 日课
date: 2015-10-13 10:22:27
tags:
---

ViewController 界面的推出，是在ViewDidLoad方法运行之后才被推出的，

所以说，ViewWillAppear和ViewDidAppear 是在ViewDidLoad之后调用的。