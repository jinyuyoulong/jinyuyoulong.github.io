---
title: swiftError
date: 2016-07-29 11:46:10
tag: swift
category: Swift
id: 15
---
value of type 'UILable' has no member 'then'

UILable 没有扩展 then的协议
fix：
extension UIView: Then{}
