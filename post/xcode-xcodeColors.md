---
title: Xcode插件XcodeColors的使用
categories: [Xcode]
date: 2016-05-27 12:51:27
tags:
---

安装：
在 管理器中搜索 下载 Xcodecolors
重启Xcode
选择load boundle

使用：
配置环境变量－>
打开Product -> Edit Scheme
选择Run->"Arguments" tab
增加一个新的Environment Variable ，命名为"XcodeColors"，值赋为YES

代码中添加：

    #define XCODE_COLORS_ESCAPE @"\033["
    #define XCODE_COLORS_RESET     XCODE_COLORS_ESCAPE @";"   // Clear any foreground or background color
    
    char * xcode_colors = getenv("XcodeColors");
    if (xcode_colors &amp;&amp; (strcmp(xcode_colors, "YES")) == 0) {
            NSLog(XCODE_COLORS_ESCAPE @"fg0,0,255;" @"Blue text" XCODE_COLORS_RESET);
    }

说明：getenv()方法为c库中的获取环境变量内容方法。