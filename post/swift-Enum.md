---
title: swift Enum
date: 2016-10-25 19:50:02
tags:
  - enum
categories:
  - Swift
id: 4
---

普通创建

```swift
enum SomeEnum: NSInteger
{
    case A
    case B
    case C
}
```



可以在Objective-C中使用的（添加@objc 关键字）

```swift
@objc enum Bear: Int {
    case Black, Grizzly, Polar
}
```
