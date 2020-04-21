---
title: OC Quartz2D 绘图
categories: [iOS]
date: 2016-02-23 12:07:20
---
如何利用Quartz2D绘制东西到view上?

首先,得有图形上下文,因为它能保存绘图信息,并且决定着绘制到什么地方去

其次,那个图形上下⽂必须跟view相关联,才能将内容绘制到view上面

⾃定义view的步骤:

(1)新建⼀个类,继承自UIView

(2)实现-(void)drawRect:(CGRect)rect⽅法.然后在这个⽅方法中 :

1)取得跟当前view相关联的图形上下文;

2)绘制相应的图形内容

3)利用图形上下文将绘制的所有内容渲染显示到view上面

1.drawRect:

（1）为什么要实现drawRect:⽅法才能绘图到view上?

因为在drawRect:⽅法中才能取得跟view相关联的图形上下文

（2）drawRect:⽅法在什么时候被调用?

当view第一次显示到屏幕上时(被加到UIWindow上显示出来)

调用view的setNeedsDisplay或者setNeedsDisplayInRect:时