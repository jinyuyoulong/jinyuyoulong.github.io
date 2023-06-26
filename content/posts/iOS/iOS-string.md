---
title: iOS NSString
categories: [iOS]
date: 2015-06-04 17:33:36
tags:
---

字符串处理：截取字符串、匹配字符串、分隔字符串

1.截取字符串

```
NSString*string=@"sdfsfsfsAdfsdf";
string = [string substringToIndex:7];//截取下标7之后的字符串 
NSLog(@"截取的值为：%@",string); 
[string substringFromIndex:2];//截取下标2之前的字符串 
NSLog(@"截取的值为：%@",string);
```

匹配字符串

```
NSString*string =@"sdfsfsfsAdfsdf"; 
NSRangerange = [stringrangeOfString:@"f"];//匹配得到的下标 
NSLog(@"rang:%@",NSStringFromRange(range)); 
string = [string substringWithRange:range];//截取范围类的字符串 
NSLog(@"截取的值为：%@",string);
```

分隔字符串

```
NSString*string =@"sdfsfsfsAdfsdf";
NSArray *array = [string componentsSeparatedByString:@"A"]; //从字符A中分隔成2个元素的数组
NSLog(@"array:%@",array); //结果是adfsfsfs和dfsdf
```