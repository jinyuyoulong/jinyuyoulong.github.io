---
title: "2020 04 21 元编程"
date: 2020-04-21T13:09:22+08:00
categories: [编程语言,设计,数据结构与算法]
---

元编程 meta programming
元编程是一种通过代码生成代码的思想，一般分为两种形式：
1. macro宏展开 或者 模板
2. runtime 运行时

宏系统分为两种：
1. 文本替换，比如 C 和 C++
2. 抽象语法树，比如 Erlang和Rust

runtime有分为 
1. Objective-C 的编译后的消息机制
2. Ruby这种通过解释器实现

runtime 都是通过根对象未能找到方法后，执行方法替换实现

参考：https://draveness.me/metaprogramming