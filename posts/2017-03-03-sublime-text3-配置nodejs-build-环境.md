---
title: sublime text3 配置nodejs build 环境
author: fan
type: post
date: 2017-03-03T15:18:23+00:00
url: /sublime-text3-配置nodejs-build-环境/
categories:
  - Nodejs
  - 工具
tags:
  - node
  - Sublime Text

---
可参考[使用Sublime Text 3 进行Python3开发][1]
  
Tools&#8211;>Build System&#8211;>New Build System 写入

    {
        "shell_cmd": "/usr/local/bin/node ${file}",
        "selector": "source.javascript",
        "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
        "working_dir": "${file_path}",
    }
    

保存为/Packages/User/node.sublime-build
  
然后选择环境为node即可

 [1]: https://www.v5u.win/archives/543