---
title: Xcode如何添加pch文件
id: 90
categories: [iOS]
date: 2015-07-14 11:31:06
tags:
---

Xcode6.0之后去掉了Precompile Prefix Header 文件，<span style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; line-height: 27.200000762939453px; text-indent: 1em;">主要原因可能在于Prefix Header大大的增加了Build的时间。没有了Prefix Header之后就要通过手动@import来手动导入头文件了，在失去了编程便利性的同时也降低了Build的时间。具体原因</span>

StackOverFlow上讨论的已经比较清晰了

[StackOverFlow:为什么xcode6没有自动创建pch文件呢？](http://stackoverflow.com/questions/24158648/why-isnt-projectname-prefix-pch-created-automatically-in-xcode-6)

### 那么如何在Xcode6中添加pch（Precompile Prefix Header）？

1，Command+N，打开新建文件窗口：ios-&gt;other-&gt;PCH file，创建一个pch文件：“工程名-Prefix.pch”

<span style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; line-height: 27.200000762939453px; text-indent: 16px; background-color: #fefefe;">    2，将building setting中的precompile header选项的路径添加“$(SRCROOT)/项目名称/pch文件名”（例如：$(SRCROOT)/LotteryFive/LotteryFive-Prefix.pch）,</span><span style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; line-height: 27.200000762939453px; text-indent: 1em;">编译一下程序，如果有错误检查一下添加的路径是否正确。</span>

&lt;

p style="margin-top: 0px; margin-bottom: 0.75em; line-height: 27.200000762939453px; text-indent: 1em; color: rgb(51, 51, 51); font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; white-space: normal;"&gt;3，将Precompile Prefix Header为YES，预编译后的pch文件会被缓存起来，可以提高编译速度

&nbsp;

[caption id="attachment_403" align="alignleft" width="600"][![pch文件build settings](http://fanjinlong.xyz/wp-content/uploads/2016/04/PCH文件-1024x475.png)](http://blog-fansrss.rhcloud.com/wp-content/uploads/2015/07/PCH文件.png) pch文件build settings[/caption]