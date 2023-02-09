---
title: "Brew的使用最佳实践"
date: 2021-04-19T14:29:57+08:00
toc: true
tags: 
  - Mac
  - brew
  - 最佳实践
---
卸载包和依赖包

安装第三方卸载工具

`brew tap beeftornado/rmtree && brew install brew-rmtree`

卸载其他软件

`brew rmtree <package>`

命令行删除文件使用 rmtrash，避免直接rm 无法找回

brew upate 更新所有的软件包

brew upgrade 更新指定的软件包
