---
title: Workspace的使用方法
tags: [xcode]
categories: [iOS]
date: 2016-07-21 16:39:53
---

1.  更改 xcode-> Preference -> Location -> Advanced -> Custom -> Relative to Workspace
2.  新建Workspace
3.  新建项目或静态库，选择 add workspace name
4.  引入路径依赖，User Header Search Paths 设为 $(BUILT_PRODUCTS_DIR) 选择递归搜索 recursive
5.  检查 scheme manage 中的项目依赖