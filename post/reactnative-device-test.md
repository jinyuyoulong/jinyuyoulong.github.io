---
title: ReactNative如何真机测试
id: 361
categories:
  - iOS
date: 2016-03-18 13:24:28
tags:
---

初始学习ReactNative 最想现在真机上一睹为快，对于非零基础的程序员，最重要的是先搞明白整个工程的创建到完结的流程，对于编程语言来说从hello world，对于一个完整的项目开发平台，则从一个最简单的dome项目开始。

iOS 真机调试

方法一：（从设备访问开发服务器）

首先，你的笔记本电脑和你的手机必须处于相同的 wifi 网络中。

打开 iOS 项目的 AppDelegate.m 文件

更改 jsCodeLocation 中的 localhost 改成你电脑的局域网IP地址

在 Xcode 中，选择你的手机作为目标设备，Run 即可

可以通过晃动设备来打开开发菜单(重载、调试等)

方法二：（使用离线包）

你也可以将应用程序本身的所有 JavaScript 代码打包。这样你可以在开发服务器没有运行时测试它，并把应用程序提交到到 AppStore。

打开 iOS / AppDelegate.m

遵循“选项 2”的说明：

取消 jsCodeLocation = [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];

在你应用程序的根目录的终端运行给定 curl 命令 （$ curl "http://localhost:8081/Game2048.bundle?platform=ios" -o main.jsbundle ）//此时应该先在本地启动服务(react-native start)

//打包项目的根目录下的 js 文件到 main.jsbundle (可以直接使用上述 curl 方法打包 javascript 即可)  $ react-native bundle [--minify]

Packager 支持几个选项：

dev(默认的 true)——设置了 **DEV** 变量的值。当是 true 时，它会打开一堆有用的警告。对于产品，它建议使用 dev = false。

minify(默认的 false)——只要不通过 UglifyJS 传输 JS 代码。

故障排除

如果 curl 命令失败，确保 packager 在运行。也尝试在它的结尾添加 ——ipv4 标志。

如果你刚刚开始了你的项目，main.jsbundle 可能不会被包含到 Xcode 项目中。要想添加它,右键单击你的项目目录，然后单击“添加文件……”——选择生成的 main.jsbundle 文件。

本文参考Jack008的blog: http://my.oschina.net/jack088/blog/515248