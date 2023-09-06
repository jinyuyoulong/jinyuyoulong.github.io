---
title: "Flutter问题点收集"
date: 2021-05-24T20:09:00+08:00
toc: true
images:
categories: [flutter,Dart]
tags: 
  - flutter
---

>前言：本质上来说flutter是一个基于2D渲染引擎的UI开发框架。

所以它具有一般的游戏引擎+原生混和开发所具有的问题。正好我现在在做U3D和iOS的混合开发，了解一点。比如：没有原生平台的硬件开发能力，无法支持应用权限管理。UI框架和原生通信的异步和同步问题。

以下是flutter的问题：
1. 图片加载问题，不同图片还好，列表动图加载，内存抖动很严重。
2. WebView开发体验不好，Flutter并没有内置的webview。需要使用原生的。