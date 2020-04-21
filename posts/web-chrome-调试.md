---
title: chrome 调试
date: 2018-11-08
categories: [工具]
---



chrome 调试

keyword: workspace,breakpoints

1. 将调试代码文件添加到Chrome 的Workspace中：Sources-->filesystem-->+Add folder to workspace-->chrome 警告框，设置允许访问—>在workspace中打开文件，直接编写，cmd+s保存-->刷新网页查看效果.
2. breakpoints: Sources-->Event Listener Breakpoints-->Mouse-->click 选中——>在调试代码出添加断点——>执行代码（例：点击button，执行js）——>使用断点调试器，R,➡️,⬇️，⬆️ 