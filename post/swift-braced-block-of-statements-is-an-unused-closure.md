---
title: braced block of statements is an unused closure
id: 330
categories: [iOS,swift]
date: 2016-03-01 15:31:45
---

使用swift写dome时xcode报一下错误：
braced block of statements is an unused closure

原因及收获：
for循环的条件语句不能有空格，如：for i=0; i&lt;3; i++ {}
其他控制语句也一样不能有空格