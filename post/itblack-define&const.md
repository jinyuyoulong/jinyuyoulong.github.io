---
title: 关键字探索 define const
tags:
  - const
  - define
id: 631
categories:
  - other technology其他技术
date: 2018-01-19 09:37:16
---

### define 单纯的代码替换，预编译时进行

### const 常数，不变的。

​    const是一个关键字。它限定一个变量不允许被改变，产生静态作用。

*   编译时进行处理

*   只分配一次内存

*   修饰关键字右边部分表示的内容不可变

      // stringConst 地址能修改，stringConst值不能修改
      NSString * const stringConst = @"I am a NSString * const string";

### static 局部变量（只在文件内使用）

*   延长被修饰变量的生命周期，程序结束才被销毁
*   只生成一份内存，只做一次初始化
*   修改变量作用域，限制在本文件内