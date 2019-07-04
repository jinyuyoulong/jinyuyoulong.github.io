---
title: terminal的显示增加色彩
tags:
  - terminal
url: 682.html
id: 682
categories:
  - Mac
date: 2018-04-04 10:16:29
---

打开 .bash_profile文件，添加：

    export GREP_OPTIONS=‘—-color=auto’ #如果没有指定，则自动选择颜色
    export CLICOLOR=1 #是否输出颜色
    export LSCOLORS=Bxfxcxdxbxegedabagacad#指定颜色
LSCOLORS此变量的值描述使用 CLICOLOR 
启用颜色时要使用哪种属性的颜色
。该字符串是
fb格式对的串联，其中f是前景色，b是
背景色。

颜色代号如下：

a黑色
b红色
c绿色
d棕色
e蓝色
f洋红色
g青色
h浅灰色
黑色粗体，通常显示为深灰色
B粗体红色
C粗体绿色
D粗体棕色，通常显示为黄色
E粗体蓝色
F粗体洋红色
G加粗青色
H加粗浅灰色; 看起来像明亮的白色
x默认前景或背景

请注意，以上是标准的ANSI颜色。实际
显示可能根据
使用中的终端的颜色能力而不同。

---

属性的顺序如下：

1.目录
2.符号链接
3.套接字
4.管道
5.可执行
6.块特殊
7.字符特殊
8.可执行与setuid位设置
9.可执行与setgid位设置
10.目录可写给其他人，粘性位
11。目录可写给其他人，没有粘性
位

默认为“exfxcxdxbxegedabagacad”，即
常规目录的
蓝色前景和默认背景，setuid执行的黑色前景和红色背景
等。