---
title: 宏定义
tags:
  - 宏定义
id: 242
categories:
  - iOS
date: 2015-09-18 15:50:23
---

<span style="font-stretch: normal; font-variant-ligatures: no-common-ligatures; color: rgb(210, 143, 90); font-family: &#39;Helvetica Neue&#39;; font-size: 14px;">#define DLOG( s, ... ) NSLog(@</span><span style="font-stretch: normal; font-variant-ligatures: no-common-ligatures; color: rgb(228, 68, 72); font-family: &#39;Helvetica Neue&#39;; font-size: 14px;">&quot;&lt; %@: (%d) &gt; %@&quot;</span><span style="color: rgb(210, 143, 90); font-family: Menlo; font-size: 11px;"><span style="font-size: 11px;">,[[NSString stringWithUTF8String:__FILE__] lastPathComponent], __LINE__, [NSString stringWithFormat:(s), ##__VA_ARGS__])</span></span>

这个宏定义是用来在打印log的时候，调试使用，可以显示当前log所在的controller名字。

先写出来，原理以后查看了再来补，