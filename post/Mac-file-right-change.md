---
title: mac文件权限修改
tags:
  - chmod
  - terminal
id: 568
categories:
  - Mac
  - 工具
date: 2017-03-13 17:20:42
---

文件或目录的访问权限分为只读，只写和可执行三种。
文件被创建时，文件所有者自动拥有对该文件的读、写和可执行权限，以便于对文件的阅读和修改。
有三种不同类型的用户可对文件或目录进行访问：文件所有者，同组用户、其他用户。

用ls -l命令显示文件或目录的详细信息，最左边的一列为文件的访问权限

例:

`$ ls -l script.swift`

`-rw-r--r--  1 fans  staff  39  3 13 16:16 script.swift`

横线代表空许可。r代表只读，w代表写，x代表可执行

这里共有10个位置。第一个字符指定了文件类型。
在通常意义上，一个目录也是一个文件。如果第一个字符是横线，表示是一个非目录的文件。如果是d，表示是一个目录。

<table>
<thead>
<tr>
  <th>-</th>
  <th>rw-</th>
  <th>r--</th>
  <th>r--</th>
</tr>
</thead>
<tbody>
<tr>
  <td>普通文件</td>
  <td>文件主</td>
  <td>组用户</td>
  <td>其他用户</td>
</tr>
</tbody>
</table>

是文件script.swift 的访问权限，表示script.swift是一个普通文件；
script.swift的属主有读写权限；与script.swift属主同组的用户只有读权限；其他用户也只有读权限。

### chmod 命令

功能：用于改变文件或目录的访问权限.用户用它控制文件或目录的访问权限.
语法：该命令有两种用法。一种是包含字母和操作符表达式的文字设定法；另一种是包含数字的数字设定法。

1.  文字设定法

    `chmod u+x script.swift`

    [详情点一下][http://blog.csdn.net/nitghost/article/details/4224034]</p>
2.  数字设定法

    略。。。知道那么多干嘛，一种还不够你用的！^_^

<p>swift研究学习
[![Swift Engineer](//pub.idqqimg.com/wpa/images/group.png "Swift Engineer")](//shang.qq.com/wpa/qunwpa?idkey=a86c7e689fa8a92f2dd8273c553cb8e78bdd3126bb8b47fc9912bb424778f4a3)