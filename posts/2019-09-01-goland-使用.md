---
title: Goland 使用
author: fan
type: post
date: 2019-09-01T11:45:59+00:00
url: /goland-使用/
categories:
  - Go
tags:
  - Go

---
做 Go 开发，一般使用的IDE是 Goland
  
安装略，自己解决。下面说安装后的事情。

  1. 配置文件，配置开发环境

goland 会自动读取 GOROOT 和 GOPATH，所以不用自己填写。我们要做的就是配置配置文件
  
创建go build配置文件：Templates&#8211;> Go Build
  
Run kind 选Directory
  
Directory 选你的main包所在文件夹
  
Output directory设置与go build -o 不相容，所以不用设置，我们使用-o参数来控制可执行文件的路径以及名字
  
Working directory保持默认就好
  
Go tool arguments 就是go build 的参数

<ol start="2">
  <li>
    debug
  </li>
</ol>

goland 的 debug 功能可以看到 整个函数链条，和当下参数的值，以及 `·s` 文件(汇编文件)的内部调用
  
单文件调试：直接点击run旁边的debug按钮，左下方有细分子项：跳过执行（步过），单步调试（步入），步出
  
整项目调试：