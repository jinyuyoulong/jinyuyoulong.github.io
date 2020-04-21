---
title: 使用sublime text 3 进行Python3开发
author: fan
type: post
date: 2017-01-23T07:22:20+00:00
url: /使用sublime-text-3-进行python3开发/
categories:
  - Python
  - 工具
tags:
  - Python
  - Sublime Text

---
    痛点1：每次编写完Python文件后都要切到terminal下输入python fileName.py命令执行文件。
    解决：mac版sublime text编辑器使用shift+command+b选择Python 直接执行文件
    

    痛点2：sublime默认执行的Python版本是系统默认的，不能直接使用Python3来执行Python文件
    解决：Tools-->Build System-->New Build System 写入：
    {
        "shell_cmd": "/usr/bin/env python3 ${file}",
        "selector": "source.python",
        "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
        "working_dir": "${file_path}",
        "env": {"PYTHONIOENCODING": "utf8"},
    }
    保存为/Packages/User/python3.sublime-build
    然后选择环境为python3即可