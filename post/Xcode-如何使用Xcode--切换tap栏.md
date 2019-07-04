---
title: 如何使用Xcode--切换tap栏
tags:
  - xcode
id: 109
categories:
  - iOS
date: 2015-07-16 11:10:27
---

切换tap栏快捷键：commend+Shift+[,] ，此方法通用于其他APP上的tap栏切换

以下为转载

转自[http://m.blog.csdn.net/blog/okmyang/38734063#](http://m.blog.csdn.net/blog/okmyang/38734063# "http://m.blog.csdn.net/blog/okmyang/38734063#")

这次我来说说怎么设置Tab来提高在xCode的工作效率。

# 我是如何使用Tab来提高效率的

## xCode的Tab是什么

诺，就是这一个东西。

![](http://ww4.sinaimg.cn/large/686e6613jw1e5b26nmyqij20oq00v0sp.jpg)

使用过各种浏览器的你一定不会陌生。对在xCode里面我们也可以开出多个页面。而且每一个页面的状态是单独保存的。

<a target="_blank" id="more" style="color: rgb(37, 143, 184); line-height: 24px; white-space: normal; margin: 0px; padding: 0px; border: 0px; outline: 0px; font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; font-size: 14px; vertical-align: baseline;"></a><span style="padding: 0px; margin: 0px; line-height: 24px; color: rgb(85, 85, 85); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; font-size: 14px;"></span><span style="font-family: Arial; line-height: 24px; background-color: rgb(237, 237, 237);"></span>

## 如何提高效率

因为在实际的代码编写过程中，我们可能需要来回的查找和阅读代码。会很自然的在多个文件中跳转编辑。这时候单个编辑页面明显拖累了速度。所以我们需要多个页面来回切换就会很爽。

如上图所示。我习惯性长开着这几个Tab。

## UI

![](http://ww3.sinaimg.cn/large/686e6613jw1e5b1quy5pij207409wt99.jpg)

如图所示，我们可以在圈起来的地方设置关键词过滤显示的文件
这样我的名为UI的Tab就只会显示storyboard。这样改UI点击起来会很方便

## Data

同理可得这个表情用来显示data model的。

![](http://ww2.sinaimg.cn/large/686e6613jw1e5b1uqa7yhj207w094mxd.jpg)

## VC

显示ViewController的

![](http://ww2.sinaimg.cn/large/686e6613jw1e5b1v4lkuyj207x0933z6.jpg)

## Debug

Debug这个Tab有些特殊。并不是我手动创建的。而且我配置了编译行为出来的。
这样每次Run的时候都会跳到这个名为Debug的Tab里面。这样做的原因是，我改了一个地方的代码。运行以后可能在其他地方挂掉了（或者在其他地方打了断点）。然后跟着进去看了看。然后想回到之前改代码的地方就会很麻烦。

![](http://ww4.sinaimg.cn/large/686e6613jw1e5b1ws3qu9j20ku0f8mzu.jpg)

这样设置了以后，就没有上述烦恼了。

# 顺便说一句

希望这些对你有所帮助。

顺便说一句：Tab直接的切换可以使用快捷键 Command + Shift + ([, ]) 其实这个快捷键适用于绝大部分有Tab的App。 都可以完成切换功能

再顺便说一句： xCode本身内存消耗很大，开Tab。感觉很是消耗内存。如果内存吃紧的话。应该去升级内存了。不然开多个Tab只会降低工作效率并不会提高。