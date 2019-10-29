---
title: iOS indexPath.item vs indexPath.row
categories: [iOS]
date: 2018-04-02 06:25:02
tags:
---

Inside NSIndexPath, the indexes are stored in a simple c array called "\_indexes" defined as NSUInteger* and the length of the array is stored in "\_length" defined as NSUInteger. The accessor "section" is an alias to "\_indexes\[0\]" and both "item" and "row" are aliases to "\_indexes\[1\]". Thus the two are functionally identical. In terms of programming style – and perhaps the definition chain – you would be better using "row" in the context of tables, and "item" in the context of collections. 在NSIndexPath中，\_indexes\[0\]位置代表的是section。\_indexes\[1\]位置代表的是row和item，所以说大体上row和item是一样的，不过row默认是用在tables中，item默认是用在collections中