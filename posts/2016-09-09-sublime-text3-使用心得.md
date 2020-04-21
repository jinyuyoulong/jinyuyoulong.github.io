---
title: Sublime Text3 使用心得
author: fan
type: post
date: 2016-09-09T06:45:12+00:00
url: /sublime-text3-使用心得/
categories:
  - 工具
tags:
  - Sublime Text

---
  1. build nodejs项目
  
    sublime text 3自带build的系统，只需要在tools->build system-> new build system&#8230;

    {
      "shell_cmd": "node $file",
      "selector": "source.js"
    }
    

保存为 node.sublime-build，就可以使用cmd+shift+b调出窗口选择node编译.
  
在keymap绑定按键：

    {
        "keys": ["ctrl+c"],
        "command": "exec",
        "args": {
          "kill": true
        }
      }
    

就可以使用快捷键ctrl+c关闭，或者手动点选tools-> cancel build中断。
  
需要编译es6的代码的话可以考虑用babel，build tools替换成

    {
      "shell_cmd": "babel-node  $file",
      "selector": "source.js"
    }
    

### 插件安装

shift+commend+p 输入install敲return/Enter，查找插件
  
我安装的插件：
  
* Babel `ES2015语法转化器`
  
* EJS `WEB所使用的模板引擎之一`
  
* emmet `提高HTML & CSS3编写速度`
  
* ConvertToUTF8 `UTF8转换`
  
*
  
插件使用教程：
  
emmet : http://www.w3cplus.com/tools/using-emmet-speed-front-end-web-development.html