---
title: vscode配置go开发环境
data: 2019-02-15
categories: [工具]
tags: [vscode]
---

下载安装 vscode，安装Go插件。在商店中搜索安装。

#### 配置 settings.json 

cmd+, ——> 用户设置/扩展 ——> Go configuration / 在 setting.json 中编辑。

参考 Sublime Text 中的 preferences.sublime-setting 很像。

在 .vscode 目录下 新建 settings.json 文件

```json
{
//setting.json
    "files.autoSave": "onWindowChange",
    "[go]": {
        "editor.insertSpaces": false,
        "editor.formatOnSave": true,
    },
    "go.goroot": "/usr/local/go",
    "go.gopath": "/User/xxx/",
    "go.buildOnSave":"package",
    "go.lintOnSave": "file",
    "go.vetOnSave": "off",
    "go.buildTags": "",
    "go.buildFlags": [],
    "go.lintFlags": [],
    "go.vetFlags": [],
    "go.coverOnSave": false,
    "go.useCodeSnippetsOnFunctionSuggest": false,
    "go.formatTool": "goreturns",
    "go.gocodeAutoBuild": true
}
```

#### 配置 tesks.json 支持 go run 命令

在 .vscode 目录下 新建 tesks.json 文件

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "run",
            "type": "shell",
            "command": "go",
            "args": [
                "run",
                "-v",
                "${file}"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }                    
        }
    ],
    "options": {
        "env": {
            "GOPATH":"/User/xxx/dev/go/golib"
        }
    },
    "presentation":{
        "echo": true,
        "reveal": "always",
        "focus": false,
        "panel": "shared",
        "showReuseMessage": true,
        "clear": false
    },
        
}
```



##### vscode安装golang.org的golint

