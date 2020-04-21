---
title: Go 语言简介
<<<<<<< HEAD:posts/2019-02-21-go-语言简介.md
author: fan
type: post
date: 2019-02-21T09:51:30+00:00
url: /go-语言简介/
categories:
  - Go
tags:
  - Go

=======
date: 2019-02-21
categories: [ Go]
>>>>>>> 9b93207d813e2b213031f967612e37c68194cf37:post/Go-语言简介.md
---
[TOC]
###  C/C++ 与 Go语言的“价值观”对照

之前看过 白明老师 在GopherChina2017的一篇演讲文章[《Go coding in go way》](http://tonybai.com/2017/04/20/go-coding-in-go-way/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)，里面提到C/C++/Go三门语言价值观，感觉很有意思，分享给大家感受一下：

C的价值观摘录

- 相信程序员：提供指针和指针运算，让C程序员天马行空的发挥
- 自己动手，丰衣足食：提供一个很小的标准库，其余的让程序员自造
- 保持语言的短小和简单
- 性能优先

C++价值观摘录

- 支持多范式，不强迫程序员使用某个特定的范式
- 不求完美，但求实用（并且立即可用）

Go价值观

- Overall Simplicity 全面的简单
- Orthogonal Composition 正交组合
- Preference in Concurrency 偏好并发

用一句话概括Go的价值观： Go is about orthogonal composition of simple concepts with preference in concurrency(Go是在偏好并发的环境下的简单概念/事物的正交组合).

##### Go 的底层语言是什么

借用大神的话来说

> 编译器就是输入源代码输出其他语言源代码的程序 

所以这个程序用什么语言实现无所谓
  
然而，一开始没有go，所以用c实现了一版go编译器，后来go语言存在了，那就可以用go再重写一遍编译器，用c写的编译器来编译这个新的编译器的源代码
  
然后就成了现在这个样子
  
你可以找找老版本看看c实现

> 2015年8月19日，Go语言Go 1.5版发布，本次更新中移除了”最后残余的C代码” 

从此 Go 实现了自举

##### Go 的市场定位

Go语言尤其适合编写网络服务相关基础设施，同时也适合开发一些工具软件和系统软件。
  
​ ——《The Go Programming Language》
  
Go 语言能吞食的一定是 PaaS 上的项目，比如一些消息缓存中间件、服务发现、服务代理、控制系统、Agent、日志收集等等，没有复杂的业务场景，也到不了特别底层（如操作系统）的中间平台层的软件项目或工具。而 C 和 C++ 会被打到更底层，Java 会被打到更上层的业务层。这是**左耳朵耗子**的一个判断。
  
用上面的标尺来量一下 Go 语言的杀手级应用 Docker，你会发现基本是一样的。
  
[学习文档][1]

 [1]: https://books.studygolang.com/gopl-zh/ch0/ch0-01.html