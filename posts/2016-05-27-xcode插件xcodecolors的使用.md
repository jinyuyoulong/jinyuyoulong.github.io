---
title: Xcode插件XcodeColors的使用
author: fan
type: post
date: 2016-05-27T12:51:27+00:00
url: /xcode插件xcodecolors的使用/
duoshuo_thread_id:
  - 6289226646893363969
  - 6289226646893363969
categories:
  - iOS
  - Mac

---
安装：
  
在 管理器中搜索 下载 Xcodecolors
  
重启Xcode
  
选择load boundle
  
使用：
  
配置环境变量－>
  
打开Product -> Edit Scheme
  
选择Run->&#8221;Arguments&#8221; tab
  
增加一个新的Environment Variable ，命名为&#8221;XcodeColors&#8221;，值赋为YES
  
代码中添加：

    #define XCODE_COLORS_ESCAPE @"\033["
    #define XCODE_COLORS_RESET     XCODE_COLORS_ESCAPE @";"   // Clear any foreground or background color
    char * xcode_colors = getenv("XcodeColors");
    if (xcode_colors && (strcmp(xcode_colors, "YES")) == 0) {
            NSLog(XCODE_COLORS_ESCAPE @"fg0,0,255;" @"Blue text" XCODE_COLORS_RESET);
    }
    

说明：getenv()方法为c库中的获取环境变量内容方法。