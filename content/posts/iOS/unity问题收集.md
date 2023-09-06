---
title: "Unity问题收集"
date: 2023-09-06T10:14:06+08:00
draft: true
toc: true
images:
categories:
  - Unity
tags: 
  - Unity
---

## ios14 启动就crash

CreateMTLLibraryFromSource

我们iOS14也出了状况，有两个表现：
1、启动就闪退，多起几次可以过去
2、启动后到某个阶段之间卡死（必卡跳不过）
XCode里看，始终是GfxDriver报错，我们渠道方发现，XCode里【BuildSetting - Packaging - Product Name】不能含有中文，有中文就出这个问题，改掉就好了。
根本原因尚不明确，个人猜测Product Name会影响Header Folder Path，可能是代码加载路径中出现中文会出问题（类似早期Unity的状况）。希望对你有帮助。