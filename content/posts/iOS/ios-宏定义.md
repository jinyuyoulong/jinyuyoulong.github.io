---
title: 宏定义
author: fan
type: post
date: 2015-09-18T07:50:23+00:00
url: /宏定义/
duoshuo_thread_id:
  - 6278603346844582658
  - 6278603346844582658
views:
  - 1
  - 1
categories:
  - iOS
tags:
  - 宏定义

---
<p style="white-space: normal;">
  <span style="font-stretch: normal; font-variant-ligatures: no-common-ligatures; color: rgb(210, 143, 90); font-family: &#39;Helvetica Neue&#39;; font-size: 14px;">#define DLOG( s, &#8230; ) NSLog(@</span><span style="font-stretch: normal; font-variant-ligatures: no-common-ligatures; color: rgb(228, 68, 72); font-family: &#39;Helvetica Neue&#39;; font-size: 14px;">"< %@: (%d) > %@"</span><span style="color: rgb(210, 143, 90); font-family: Menlo; font-size: 11px;"><span style="font-size: 11px;">,[[NSString stringWithUTF8String:__FILE__] lastPathComponent], __LINE__, [NSString stringWithFormat:(s), ##__VA_ARGS__])</span></span>
</p>

<p style="white-space: normal;">
</p>

<p style="white-space: normal;">
  这个宏定义是用来在打印log的时候，调试使用，可以显示当前log所在的controller名字。
</p>

<p style="white-space: normal;">
  先写出来，原理以后查看了再来补，
</p>