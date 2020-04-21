---
title: indexPath.item vs indexPath.row
author: fan
type: post
date: 2018-04-02T06:25:02+00:00
url: /indexpath-item-vs-indexpath-row/
categories:
  - iOS
format: aside

---
Inside NSIndexPath, the indexes are stored in a simple c array called &#8220;\_indexes&#8221; defined as NSUInteger* and the length of the array is stored in &#8220;\_length&#8221; defined as NSUInteger. The accessor &#8220;section&#8221; is an alias to &#8220;\_indexes[0]&#8221; and both &#8220;item&#8221; and &#8220;row&#8221; are aliases to &#8220;\_indexes[1]&#8221;. Thus the two are functionally identical.
  
In terms of programming style – and perhaps the definition chain – you would be better using &#8220;row&#8221; in the context of tables, and &#8220;item&#8221; in the context of collections.
  
在NSIndexPath中，\_indexes[0]位置代表的是section。\_indexes[1]位置代表的是row和item，所以说大体上row和item是一样的，不过row默认是用在tables中，item默认是用在collections中