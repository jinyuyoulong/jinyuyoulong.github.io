---
title: code review
date: 2018-09-10
categories: [system]
---



**Code Review的好处我觉得不用多说了，主要是让你的代码可以更好的组织起来，有更易读，有更高的维护性，同时可以达到知识共享，找到bug只是其中的副产品**。

**我个人认为代码有这几种级别：**1）可编译，2）可运行，3）可测试，4）可读，5）可维护，6）可重用。通过自动化测试的代码只能达到第3）级，而通过Code Review的代码少会在第4）级甚至更高。

在Amazon，开发工程师都会被教育拿到需求后一定要问——“为什么要做？业务影响度有多大？有多少用户受益？”，



#### review实施思路

先Review设计实现思路，然后Review设计模式，接着Review成形的骨干代码，最后Review完成的代码，如果程序复杂的话，需要拆成几个单元或模块分别Review。当然，最佳的practice是，每次Review的代码应该在1000行以内，时间不能超过一部电影的时间——1.5小时（因为据说那个一个正常人的膀胱可以容纳尿液的最长限度）

#### 1.- 经常进行Code Review

#### 2.- Code Review不要太正式，而且要短

#### 3.- 尽可能的让不同的人Reivew你的代码

#### 4.- 保持积极的正面的态度

 5.- 学会享受Code Reivew

https://coolshell.cn/articles/1302.html



review工具

**1. Review board:**

**Codestriker:**

**Groogle:**：

- 各式各样语言的语法高亮。
- 支持整个版本树的比较。
- 支持当个文件不同版本的diff功能，并有一个图形的版本树。
- 邮件通知所有的Reivew的人当前的状态。
- 认证机制。



**4. Rietveld:**

[Review board](http://www.review-board.org/) 很像。它也是一个基于Web的应用，并在[Google App Engine](http://code.google.com/appengine/) 上。

**5. JCR**

基于WEB界面的最初设计给Reivew Java 语言的

[JCR](http://jcodereview.sourceforge.net/) 主要想协助：

- **审查者**。所有的代码更改都会被高亮，以及大多数语言的语法高亮。Code extracts 可以显示代码评审意见。如果你正在Review Java的代码，你可以点击代码中的类名来查看相关的类的声明。
- **项目所有者**。可以 轻松创建并配置需要Review的项目，并不需要集成任何的软件配置管理系统（SCM）。
- **流程信仰者**。 所有的评语都会被记录在数据库中，并且会有状态报告，以及各种各样的统计。
- **架构师和开发者**。 这个系统也可以让我们查看属于单个文件的评语，这样有利于我们重构代码。

[JCR](http://jcodereview.sourceforge.net/) 主要面对的是大型的项目，或是非常正式的代码评审，从这方面看来，他并不像上面的那些工具。



**Jupiter**

它是一个Eclipse IDE 的插件。

Gerrit

使用 [Git](https://www.oschina.net/p/git) 作为底层版本控制系统。它分支自[Rietveld](http://www.oschina.net/p/rietveld)，作者为Google公司的Shawn Pearce，原先是为了管理Android计划而产生。

Gerrit实际上一个Git服务器，它为在其服务器上托管的Git仓库提供一系列权限控制，以及一个用来做Code Review是Web前台页面。当然，其主要功能就是用来做Code Review。