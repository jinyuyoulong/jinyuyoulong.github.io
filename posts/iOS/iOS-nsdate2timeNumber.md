---
title: NSDate和时间戳互转
tags: [NSDate,时间戳]
categories: [iOS]
date: 2015-08-28 16:53:17
---

## iOS 将时间NSDate转化为毫秒时间戳

对于将NSDate类型转换为时间戳，相信大家肯定都会，这样的示例代码，在百度等搜索引擎上面一搜索就是一大篇的东西，但是，大家有没有注意到的是 通过那些方法转换得到的时间戳是 10位的数值，这个数值在转化为 NSDate类型的时候，就会出点儿错，你会发现，每一个时间的 毫秒都是为000的；&nbsp;

而正确的应该是下面这样的输出：&nbsp;

&nbsp;&nbsp;&nbsp; 好了，接下来就是问题所在了：其实呢，并不是我们代码出错了，而是因为 [[NSDate date] timeIntervalSince1970] 虽然可以获取到后面的毫秒、微秒 ，但是在保存的时候省略掉了。如一个时间戳不省略的情况下为 1395399556.862046 ，省略掉后为一般所见 1395399556 。所以想取得毫秒时用获取到的时间戳 *1000 ，想取得微秒时 用取到的时间戳 * 1000 * 1000 。这样就解释了上面的10位数值的问题，当你取毫秒的时候，就会变成13位数值了。我想这样大家应该明白了吧！&nbsp;
&nbsp;&nbsp;&nbsp; 当然，说了 这么多理论性的东西，为的就是我们接下来会附上的代码的：&nbsp;
将这段代码写在 你需要获取时间戳和转换的地方，而我因为是简单示范，就放在-viewDidload里面的。&nbsp;

long long time = [self getDateTimeTOMilliSeconds:[NSDate date]];
NSLog(@&quot;%llu&quot;,time);

NSDate *dat = [self getDateTimeFromMilliSeconds:time];
NSDateFormatter * formatter = [[NSDateFormatter alloc ] init];
[formatter setDateFormat:@&quot;YYYY-MM-dd hh:mm:ss.SSS&quot;];
NSString *date = [formatter stringFromDate:dat];
NSString *timeLocal = [[NSString alloc] initWithFormat:@&quot;%@&quot;, date];
NSLog(@&quot;n%@&quot;, timeLocal);

里面包含了自己写出来了2个小函数，这2个函数呢，是互逆的：&nbsp;

//将时间戳转换为NSDate类型
-(NSDate *)getDateTimeFromMilliSeconds:(long long) miliSeconds
{
NSTimeInterval tempMilli = miliSeconds;
NSTimeInterval seconds = tempMilli/1000.0;//这里的.0一定要加上，不然除下来的数据会被截断导致时间不一致
NSLog(@&quot;传入的时间戳=%f&quot;,seconds);
return [NSDate dateWithTimeIntervalSince1970:seconds];
}

//将NSDate类型的时间转换为时间戳,从1970/1/1开始
-(long long)getDateTimeTOMilliSeconds:(NSDate *)datetime
{
NSTimeInterval interval = [datetime timeIntervalSince1970];
NSLog(@&quot;转换的时间戳=%f&quot;,interval);
long long totalMilliseconds = interval*1000 ;
NSLog(@&quot;totalMilliseconds=%llu&quot;,totalMilliseconds);
return totalMilliseconds;
}

这样，你就可以得到你想要的13位时间戳，并且从这个时间戳里面获取正确的时间（精确到毫秒哟！）。&nbsp;

本文转自晓龙歌：http://longlinyisheng.lofter.com/post/3ca1cc_59c458a