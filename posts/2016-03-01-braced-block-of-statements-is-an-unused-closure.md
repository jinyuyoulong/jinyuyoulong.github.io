---
title: braced block of statements is an unused closure
author: fan
type: post
date: 2016-03-01T07:31:45+00:00
url: /braced-block-of-statements-is-an-unused-closure/
duoshuo_thread_id:
  - 6278603394655453954
  - 6278603394655453954
categories:
  - iOS
  - swift

---
使用swift写dome时xcode报一下错误：
  
braced block of statements is an unused closure

原因及收获：
  
for循环的条件语句不能有空格，如：for i=0; i<3; i++ {}
  
其他控制语句也一样不能有空格