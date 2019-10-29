---
title: Goland 使用
date: 2019-07-12
categories:
  - Go
---

做 Go 开发，一般使用的IDE是 Goland

安装略，自己解决。下面说安装后的事情。

1. 配置文件，配置开发环境

goland 会自动读取 GOROOT 和 GOPATH，所以不用自己填写。我们要做的就是配置配置文件

创建go build配置文件：Templates--> Go Build
Run kind 选Directory
Directory 选你的main包所在文件夹
Output directory设置与go build -o 不相容，所以不用设置，我们使用-o参数来控制可执行文件的路径以及名字
Working directory保持默认就好
Go tool arguments 就是go build 的参数