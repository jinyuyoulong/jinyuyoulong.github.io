---
title: python-sublime
date: 2017-11-29 17:29:24
tags: [sublime text,python]
categories: [Python]
---

sublime text 下的Python编译环境设置

file name : python3.sublime-build
```
{

	"shell_cmd": "Python编译器的路径 ${file}",
	"selector" :"source.python",
	"file_regex":"^(...*?):[0-9]:?([0-9]*)",
	"working_dir":"${file_path}",
	"env": {"PYTHONIOENCODING": "utf8"},
}
```
