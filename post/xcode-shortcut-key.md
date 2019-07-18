---
title: Xcode快捷键
tags:
  - xcode
  - 快捷键
id: 372
categories:
  - iOS
date: 2016-03-29 23:50:12
---

常用xcode快捷键

    整行移动 option+commend+[]
    当前页快速定位：ctl+6
    项目中file间快速定位：shift+cmd+o
    删除光标右边的字符：Ctrl+D
    删除本行：Ctrl+K
    光标移动到上一行：Ctrl+P
    移动光标到下一行：Ctrl + N
    折叠全部方法实现：shift+option+commend+left
    显示自动提示：ESC
    变量重命名：ctl+cmd+e (Edit All In Scop)
    `</pre>

    crl+i 对齐代码
    1.如果是在打开的文档范围内：
    查找： Command+ F
    替换： Command+Option+F
    Replace All 是全部替换本文档范围内的字符串
    Replace 是替换当前字符串
    Replace &amp; Find是边查找边替换

    2.如果是全局查找和替换
    查找：点击左边工具栏里面的“放大镜”按钮 或者 Shift+Command +F
    替换：点击左边工具栏里面的“放大镜”按钮，然后左边 Find 改为 Replace即可。或者 Shift+Option+Command+F
    3.变量重命名
    Menu: Editor -&gt; Edit All In Scope (also shows key binding)
    Keyboard Shortcut: Control-Command-E
    If you want you can change this key binding on Preferences -&gt; Key Bindings -&gt; search for "Edit all in scope".

    <pre>`1\. 文件

CMD + N: 新建文件
CMD + SHIFT + N: 新建项目
CMD + O: 打开
CMD + S: 保存
CMD + SHIFT + S: 另存为
CMD + W: 关闭窗口
CMD + SHIFT + W: 关闭文件

1.  编辑

CMD + [: 左缩进
CMD + ]: 右缩进

CMD + CTRL + LEFT: 折叠
CMD + CTRL + RIGHT: 取消折叠
CMD + CTRL + TOP: 折叠全部函数
CMD + CTRL + BOTTOM: 取消全部函数折叠
CTRL + U: 取消全部折叠

CMD + D: 添加书签
CMD + /: 注释或取消注释

CTRL + .: 参数提示
ESC: 自动提示列表

1.  调试

CMD + : 设置或取消断点
CMD + OPT + : 允许或禁用当前断点
CMD + OPT + B: 查看全部断点

CMD + RETURN: 编译并运行（根据设置决定是否启用断点）
CMD + R: 编译并运行（不触发断点）
CMD + Y: 编译并调试（触发断点）
CMD + SHIFT + RETURN: 终止运行或调试

CMD + B: 编译
CMD + SHIFT + K: 清理

1.  窗体

CMD + SHIFT + B: 编译窗口
CMD + SHIFT + Y: 调试代码窗口
CMD + SHIFT + R: 调试控制台
CMD + SHIFT + E: 主编辑窗口调整

1.  帮助

CMD + OPT + ?: 开发手册
CMD + CTRL + ?: 快速帮助
下面也是一些有用的快捷键(转自http://www.cppblog.com/brucejini/archive/2010/12/24/137367.html)

Command + Shift + E ：扩展编辑器
Command + [ ：左移代码块
Command + ] ：右移代码块
Tab ：接受代码提示
Esc ：显示代码提示菜单
Ctrl + . （句点）：循环浏览代码提示
Shift + Ctrl + . （句点）：反向循环浏览代码提示
Ctrl + / ：移动到代码提示中的下一个占位符
Command + Ctrl + S ：创建快照

Ctrl + F ：前移光标
Ctrl + B ：后移光标
Ctrl + P ：移动光标到上一行
Ctrl + N：移动光标到下一行
Ctrl + A : 移动光标到本行行首
Ctrl + E : 移动光标到本行行尾
Ctrl + T ：交换光标左右两边的字符
Ctrl + D：删除光标右边的字符
Ctrl + K ：删除本行
Ctrl + L : 将插入点置于窗口正中
Command + Alt + D：显示open quickly 窗口
Command + Alt + 上方向键 ：打开配套文件
Command + D ：添加书签
Option + 双击：在文档中搜索
Command + Y ：以调试方式运行程序
Command + Alt + P ： 继续（在调试中）
Command + Alt + 0 ：跳过
Command + Alt + I ：跳入
Command + Alt + T ：跳出