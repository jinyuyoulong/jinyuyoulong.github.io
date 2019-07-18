---
title: swift中weak和unowned的区别
tags:
  - unowned
  - weak
id: 528
categories:
  - iOS
  - swift
date: 2016-12-13 16:34:00
---

weak和unowned都是解决循环引用的关键字
区别：
如果您是一直写 Objective-C 过来的，那么从表面的行为上来说 unowned 更像以前的 unsafe_unretained，而 weak 就是以前的 weak。
用通俗的话说，就是 unowned 设置以后即使它原来引用的内容已经被释放了，它仍然会保持对被已经释放了的对象的一个 "无效的" 引用，它不能是 Optional 值，也不会被指向 nil。如果你尝试调用这个引用的方法或者访问成员属性的话，程序就会崩溃。
而 weak 则友好一些，在引用的内容被释放后，标记为 weak 的成员将会自动地变成 nil (因此被标记为 @weak 的变量一定需要是 Optional 值)。
`关于两者使用的选择，Apple 给我们的建议是如果能够确定在访问时不会已被释放的话，尽量使用 unowned，如果存在被释放的可能，那就选择用 weak。`