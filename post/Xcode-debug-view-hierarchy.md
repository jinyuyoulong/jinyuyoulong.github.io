---
title: Xcode-debug-view-hierarchy
date: 2018-08-03 10:34:49
tag: Xcode
category: iOS
---

### Xcode 教程之调试视图层次结构

Xcode开发，当我们需要调整/检查UI时正确的处理方式是什么？

答案：debug view hierarchy

![debug view hierarchy](http://ocnjk5c7r.bkt.clouddn.com/image/iOS/debug-view-hierarchy.png)



P.s. 下面是为什么要使用debug view hierarchy，没时间的读者自行略过

很多人知道

很多人不知道

很多人知道仅仅了解了一下

少部分的人知道了解，并经常用它辅助开发。

范子属于知道作为新功能仅仅了解了一下。包括之前的Mac软件reveal。

因为实际的开发过程中，并不是很关心UI的处理，毕竟前期要先保证业务逻辑正确，后期还有调整&测试UI的过程。

然而在这次的产品在上线之前临时提出调整UI的需求，在调整UI的过程中，让范子重新审视了一下自己画UI的过程是否合理。

其实范子之前就知道自己画UI很不用心，或者说没有给予足够的重视，在整个产品开发过程中，经常出现后期调整，耽误工程进度的情况。

这次的反思并不是因为影响进度，而是基于自身的编码习惯的反思审视。我们可以通过debug view hierarchy一次完成完美的代码布局，并以此优化自己代码布局逻辑，其实是有助于提升自己的编码水平的。

以前是因为没有合适的工具比如reveal收费昂贵。现在Xcode早就原生支持了，那么我们也就不应错过这个可以提升效率的工具。

完！