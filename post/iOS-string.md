---
title: iOS NSString 字符串处理：截取字符串、匹配字符串、分隔字符串
categories: [iOS]
date: 2015-06-04 17:33:36
tags:
---

<span style="font-size:12px;outline: none; line-height: 19.5px; color: rgb(51, 51, 51); font-family: arial, 宋体; white-space: normal; background-color: rgb(255, 255, 255);">1.截取字符串</span>

<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSString*string =@&quot;sdfsfsfsAdfsdf&quot;;</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">string = [string&nbsp;substringToIndex:7];//截取下标7之后的字符串</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSLog(@&quot;截取的值为：%@&quot;,string);</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">[string&nbsp;substringFromIndex:2];//截取下标2之前的字符串</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSLog(@&quot;截取的值为：%@&quot;,string);</span>

<span style="font-size:12px;outline: none; line-height: 19.5px; color: rgb(51, 51, 51); font-family: arial, 宋体; white-space: normal; background-color: rgb(255, 255, 255);">2.匹配字符串</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSString*string =@&quot;sdfsfsfsAdfsdf&quot;;</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSRangerange = [stringrangeOfString:@&quot;f&quot;];//匹配得到的下标</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSLog(@&quot;rang:%@&quot;,NSStringFromRange(range));</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">string = [string&nbsp;substringWithRange:range];//截取范围类的字符串</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSLog(@&quot;截取的值为：%@&quot;,string);</span>

<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">3.分隔字符串</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSString*string =@&quot;sdfsfsfsAdfsdf&quot;;</span>

<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSArray&nbsp;*array = [string&nbsp;componentsSeparatedByString:@&quot;A&quot;]; //从字符A中分隔成2个元素的数组</span>
<span style="color: rgb(51, 51, 51); font-family: arial, 宋体; font-size: small; line-height: 19.5px; background-color: rgb(255, 255, 255);">NSLog(@&quot;array:%@&quot;,array); //结果是adfsfsfs和dfsdf</span>