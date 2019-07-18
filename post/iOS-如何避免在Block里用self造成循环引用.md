---
title: 如何避免在Block里用self造成循环引用
id: 62
categories:
  - iOS
date: 2015-05-15 16:00:00
tags:
---

本文原引于[Bannings的专栏博客](http://blog.csdn.net/zhangao0086/article/details/38273239 "避免block中self循环引用")

一般来说我们总会在设置Block之后，在合适的时间回调Block，而不希望回调Block的时候Block已经被释放了，所以我们需要对Block进行copy，copy到堆中，以便后用。

当一个Block被Copy的时候，如果你在Block里进行了一些调用，那么将会有一个强引用指向这些调用方法的调用者，有两个规则：

*   如果你是通过引用来访问一个实例变量，那么将强引用至self

*   如果你是通过值来访问一个实例变量，那么将直接强引用至这个“值”变量

苹果官方文档里有两个例子来说明这两种情况：

![](http://img.blog.csdn.net/20140729170542000?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvemhhbmdhbzAwODY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

上面第一种情况相当于用self.xxx来访问实例变量，所以强引用指向了self；第二种情况把实例变量变成了本地临时变量，强引用将直接指向这个本地的临时变量。大多数情况下，我们只用处理第一种情况就行了，因为第二种情况虽然会造成循环引用，但是临时变量很快就被释放了，不会造成真正的循环引用。要避免强引用到self的话，用__weak把self重新引用一下就行了，像这样：

1.  <span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">__weak&nbsp;</span><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: rgb(0, 0, 255); background-color: inherit; font-weight: bold;">ViewController</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;*weakSelf&nbsp;=&nbsp;</span><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: rgb(0, 0, 255); background-color: inherit; font-weight: bold;">self</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">; &nbsp;</span></span>