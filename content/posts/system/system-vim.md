---
title: vim
tags: [vim]
categories: [System]
date: 2016-04-18 17:26:21
---



Vim

自带教程 终端输入 `vimtutor`

两种模式状态
1. 命令模式
2. 编辑模式
### 命令模式下的操作
- dd 删除一行;三行：3dd
-  y复制
-  d()剪切
-  p(paste)粘贴
- :wq 或 ZZ 或 保存退出 :q! 强制退出
- / 搜索   命令模式下 `/user` 搜索 user 关键字
- i 所有非hjkl的字符 进入编辑模式

### 编辑模式
文字编辑器

分屏操作
:vsp 垂直分屏
:sp 水平分屏
:close Ctrl-w c 关闭当前窗口
:only 只保留当前窗口
ctrl+w + 当前窗口增高一行
ctrl+w > 当前窗口增宽一列
ctrl+w 切换到下一个窗
