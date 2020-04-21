---
title: ternimal
categories: [Mac,工具]
date: 2018-05-18 08:53:16
tags:
---

暴力删除文件：输入 sudo rm -rf .Trash 再输入密码后 Enter 。 mac 设置软件安装安全级别 sudo spctl --master-disable 文件权限修改

1. 文字设定法 　　chmod \[who\] \[+ | - | =\] \[mode\] 文件名? 

2. mkdir code

```
修改权限的命令格式 
chmod [<权限范围><权限操作><具体权限>] [文件或目录…]

<权限范围> 
u：User，即文件或目录的拥有者。 
g：Group，即文件或目录的所属群组。 
o：Other，除了文件或目录拥有者或所属群组之外，其他用户皆属于这个范围。 
a：All，即全部的用户，包含拥有者，所属群组以及其他用户。

<权限操作> 
+：表示增加权限 
- ：表示取消权限 
=：表示唯一设定权限

<具体权限> 
r：表示可读取 
w：表示可写入 
x ：表示可执行

例：chmod o+w 111.txt
```
打开当前文件夹 open . 打开当前文件用指定的软件 open -a Sublime\ Text Podfile (open -a app\_name file\_name)
