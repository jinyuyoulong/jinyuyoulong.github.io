---
title: use sublime Text
date: 2016-08-10
categoties: [工具]
---
### 如何设置折行 
'将配置文件里 添加word_wrap:true 字段'
```
{
	"color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
	"font_size": 13,
	"word_wrap": true,
	"ignored_packages":
	[
		"Vintage"
	]
}
```
```
痛点1：每次编写完Python文件后都要切到terminal下输入python fileName.py命令执行文件。
解决：mac版sublime text编辑器使用shift+command+b选择Python 直接执行文件
```

```
痛点2：sublime默认执行的Python版本是系统默认的，不能直接使用Python3来执行Python文件
解决：Tools-->Build System-->New Build System 写入：
{
	"shell_cmd": "/usr/local/homebrew/bin/python3 ${file}",
	"selector" :"source.python",
	"file_regex":"^(...*?):[0-9]:?([0-9]*)",
	"working_dir":"${file_path}",
	"env": {"PYTHONIOENCODING": "utf8"},
}
保存为/Packages/User/python3.sublime-build
然后选择环境为python3即可

ps: `env` //设置编码格式
`shell_cmd` 使用的路径，通过在terminal中执行which Python3 获得
```

