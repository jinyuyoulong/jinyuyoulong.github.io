---
title: Workspace的使用方法
author: fan
type: post
date: 2016-07-21T08:39:53+00:00
url: /workspace的使用方法/
duoshuo_thread_id:
  - 6309695198343463681
  - 6309695198343463681
categories:
  - iOS
tags:
  - Workspace
  - xcode

---
  1. 更改 xcode-> Preference -> Location -> Advanced -> Custom -> Relative to Workspace
  2. 新建Workspace
  3. 新建项目或静态库，选择 add workspace name
  4. 引入路径依赖，User Header Search Paths 设为 $(BUILT\_PRODUCTS\_DIR) 选择递归搜索 recursive
  5. 检查 scheme manage 中的项目依赖