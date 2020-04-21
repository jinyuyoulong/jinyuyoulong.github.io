---
title: Objective-c NSClassFromString 使用方法
author: fan
type: post
date: 2015-09-14T03:58:58+00:00
url: /objective-c-nsclassfromstring-使用方法/
duoshuo_thread_id:
  - 6278603345762452226
  - 6278603345762452226
views:
  - 2
  - 2
categories:
  - iOS
---

NSClassFromString 是一个很有用的东西，尤其在进行 iPhone toolchain 的开发上。

正常来说，

```
id myObj = [[NSClassFromString(@"MySpecialClass") alloc] init];
```

和

```
id myObj = [[MySpecialClass alloc] init];
```

是一样的。但是，如果你的程序中并不存在 MySpecialClass 这个类，下面的写法会出错，而上面的写法只是返回一个空对象而已。

因此，在某些情况下，可以使用 NSClassFromString 来进行你不确定的类的初始化。

比如在 iPhone 中，NSTask 可能就会出现这种情况，所以在你需要使用 NSTask 时，最好使用：

```
[[NSClassFromString(@"NSTask") .....]]
```

而不要直接使用 [NSTask ...] 这种写法。

**NSClassFromString 的好处是：**

弱化连接，因此并不会把没有的 Framework 也 link 到程序中。

不需要使用 import，因为类是动态加载的，只要存在就可以加载。因此如果你的 toolchain 中没有某个类的头文件定义，而你确信这个类是可以用的，那么也可以用这种方法