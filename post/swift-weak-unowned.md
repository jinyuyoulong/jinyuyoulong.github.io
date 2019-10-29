---
title: weak-unowned
date: 2016-09-19 18:11:47
tags: [swift]
categories: [Swift]
---

### swift weak和unowned 的区别

`unowned` 设置以后即使它原来引用的内容已经被释放了，它仍然会保持对被已经释放了的对象的一个 "无效的" 引用，它不能是 Optional 值，也不会被指向 `nil`。如果你尝试调用这个引用的方法或者访问成员属性的话，程序就会崩溃。而 `weak` 则友好一些，在引用的内容被释放后，标记为 `weak` 的成员将会自动地变成 `nil` (因此被标记为 @`weak` 的变量一定需要是 Optional 值)。关于两者使用的选择，Apple 给我们的建议是如果能够确定在访问时不会已被释放的话，尽量使用 `unowned`，如果存在被释放的可能，那就选择用 `weak`。