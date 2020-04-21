---
title: NSData转int
date: 2015-04-29 14:03:07
categories: [iOS]
---
```
有一种借助string的方法，经验证不对，找了半天终于找到了一个合适的，可是没有看的太明白，特补充记录在此。
1.int -> data
int i = 1;
NSData *data = [NSData dataWithBytes: &i length: sizeof(i)];//不多解释，不明白请留言
2.data -> int
int i;
[data getBytes: &i length: sizeof(i)];//必须要事先声明 int 变量，此处是将data里的数据赋值到 int变量 i 的地址里。
```

