---
title: node-gyp是什么
author: fan
type: post
date: 2019-01-31T02:57:56+00:00
url: /node-gyp是什么/
categories:
  - Nodejs

---
#### GYP

GYP是一种构建自动化工具。 GYP由Google创建，用于生成用于构建Chromium Web浏览器的本机IDE项目文件，并使用BSD软件许可证作为开源软件获得许可。 GYP的功能类似于CMake构建工具。 GYP处理包含JSON字典的文件，以生成一个或多个目标项目make文件。
  
操作系统： macOS, Linux, Solaris, FreeBSD, OpenBSD, Windows
  
编写时间： Python
  
许可协议： BSD license
  
原著者： Mark Mentovai
  
长久以来 linux 的二进制分发一直是巨坑，npm 为了方便干脆就直接源码分发，用户装的时候再现场编译。
  
Google使用过很多处理平台无关的项目构建系统，比如Scons，CMake。在实际使用中这些并不能满足需求。开发复杂的应用程序时，在Mac上Xcode更加适合，而Windows上Visual Studio更是无二之选。gyp是为Chromium项目创建的项目生成工具，生成项目文件后就可以调用GCC, vsbuild, xcode等编译平台来编译。从平台无关的配置生成平台相关的Visual Studio、Xcode、Makefile的项目文件。这样一来我们就不需要花额外的时间处理每个平台不同的项目配置以及项目之间的依赖关系。

#### node下的gyp

至于为什么要有node-gyp，是由于node程序中需要调用一些其他语言编写的工具甚至是dll，需要先编译一下，否则就会有跨平台的问题，例如在windows上运行的软件copy到mac上就不能用了，但是如果源码支持，编译一下，在mac上还是可以用的。node-gyp在较新的Node版本中都是自带的（平台相关），用来编译原生C++模块。