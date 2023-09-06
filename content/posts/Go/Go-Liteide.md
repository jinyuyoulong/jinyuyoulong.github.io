---
title: "Go Liteide IDE"
date: 2019-08-02T16:33:56+08:00
categories: [工具]
tags: [IDE]
---

[TOC]

### liteide是专门为go编写的一个基于qt5的IDE，免费开源跨平台。

*LiteIDE 是一个轻量级的开源跨平台 Go语言 IDE.* 作者: 七叶 (visualfc)

支持 Windows，Linux，Mac。

下载地址：https://github.com/visualfc/liteide.git

或命令行安装：`brew search liteide`

### 配置环境变量

1. 切换当前环境 > system—> darwin64-home, 点击旁边的小灰框(编辑当前环境)
2. 在打开的文件中设置 go 环境： GOROOT, GOPATH,GOBIN, GOPROXY
3. 注意查看下方的"事件记录" 输出日志，确认不在有报错

### 编译运行

BR : go build & run

R : 直接运行可执行文件

FR : go run file.go

B : go build

### 调试

用 [LiteIDE](https://github.com/visualfc/liteide) 可以方便调试 Go 程序，它是用的 GDB 调试的，如果没有安装 GDB 的话，运行 “调试” 就会提示：

Mac没有内置gdb，所以需要使用brew安装，但是Mac又不信任 gdb ，所以还要生成信任证书给gdb用。

参考：shttps://windmt.com/2016/01/07/installing-gdb-on-macos/ 



2.4 设置编译选项及编译

编译->编译配置，设置编译参数。在BUILDARGS添加**-gcflags "-N -l"**，目的是去掉编译优化，方便调试。

按F5启动调试，程序在main函数处停止

通过F10单步调试，可以看到i、j的变化（好像会稍微延迟那么0.X秒）
