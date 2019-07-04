---
title: Xcode7 恢复代码折叠功能
id: 393
categories:
  - iOS
date: 2016-04-08 18:14:53
tags:
---

升级到Xcode7后，发现代码折叠功能不见了！！！
苹果默认把这个功能禁掉了：在Xcode菜单里选择Preference——Text Editing，你会发现里面有一个“code folding ribbon”，勾选它就能恢复代码折叠功能了。

然后通过菜单Editor——Code Folding，你就可以使用你需要的折叠功能。

<table>
<thead>
<tr>
  <th>相关快捷键：</th>
</tr>
</thead>
<tbody>
<tr>
  <td>局部折叠（折叠一个函数）                 ：Command+Option+Left/Right</td>
</tr>
<tr>
  <td>全局折叠（折叠当前文件下的全部函数）：Shift+Command+Option+Left/Right</td>
</tr>
<tr>
  <td>折叠注释块：（/* */之间的文字）       ： Ctrl+Shift+Command+Left/Right</td>
</tr>
</tbody>
</table>