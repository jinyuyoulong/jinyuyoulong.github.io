---
title: NSDate和时间戳互转
author: fan
type: post
date: 2015-08-28T08:53:17+00:00
url: /nsdate和时间戳互转/
duoshuo_thread_id:
  - 6278603325986308865
  - 6278603325986308865
views:
  - 6
  - 6
categories:
  - iOS
tags:
  - iOS
  - NSDate

---
<h2 class="ttl" style="margin: 0px 0px 15px; padding: 0px; font-size: 20px; font-weight: normal; line-height: 30px;">
  iOS 将时间NSDate转化为毫秒时间戳
</h2>

对于将NSDate类型转换为时间戳，相信大家肯定都会，这样的示例代码，在百度等搜索引擎上面一搜索就是一大篇的东西，但是，大家有没有注意到的是 通过那些方法转换得到的时间戳是 10位的数值，这个数值在转化为 NSDate类型的时候，就会出点儿错，你会发现，每一个时间的 毫秒都是为000的； 

而正确的应该是下面这样的输出： 

    好了，接下来就是问题所在了：其实呢，并不是我们代码出错了，而是因为 [[NSDate date] timeIntervalSince1970] 虽然可以获取到后面的毫秒、微秒 ，但是在保存的时候省略掉了。如一个时间戳不省略的情况下为 1395399556.862046 ，省略掉后为一般所见 1395399556 。所以想取得毫秒时用获取到的时间戳 \*1000 ，想取得微秒时 用取到的时间戳 \* 1000 * 1000 。这样就解释了上面的10位数值的问题，当你取毫秒的时候，就会变成13位数值了。我想这样大家应该明白了吧！   
    当然，说了 这么多理论性的东西，为的就是我们接下来会附上的代码的：   
将这段代码写在 你需要获取时间戳和转换的地方，而我因为是简单示范，就放在-viewDidload里面的。 

<p style="margin-top: 0px; margin-bottom: 20px; padding: 0px;">
  long long time = [self getDateTimeTOMilliSeconds:[NSDate date]];<br />NSLog(@&#8221;%llu&#8221;,time);
</p>

NSDate *dat = [self getDateTimeFromMilliSeconds:time];  
NSDateFormatter * formatter = [[NSDateFormatter alloc ] init];  
[formatter setDateFormat:@&#8221;YYYY-MM-dd hh:mm:ss.SSS&#8221;];  
NSString *date = [formatter stringFromDate:dat];  
NSString *timeLocal = [[NSString alloc] initWithFormat:@&#8221;%@&#8221;, date];  
NSLog(@&#8221;n%@&#8221;, timeLocal);
  
里面包含了自己写出来了2个小函数，这2个函数呢，是互逆的： 

<
  
p style=&#8221;margin-top: 0px; margin-bottom: 20px; padding: 0px;&#8221;>//将时间戳转换为NSDate类型  
-(NSDate _)getDateTimeFromMilliSeconds:(long long) miliSeconds  
{  
NSTimeInterval tempMilli = miliSeconds;  
NSTimeInterval seconds = tempMilli/1000.0;//这里的.0一定要加上，不然除下来的数据会被截断导致时间不一致  
NSLog(@&#8221;传入的时间戳=%f&#8221;,seconds);  
return [NSDate dateWithTimeIntervalSince1970:seconds];  
}</p> 

//将NSDate类型的时间转换为时间戳,从1970/1/1开始  
-(long long)getDateTimeTOMilliSeconds:(NSDate *)datetime  
{  
NSTimeInterval interval = [datetime timeIntervalSince1970];  
NSLog(@&#8221;转换的时间戳=%f&#8221;,interval);  
long long totalMilliseconds = interval</em>1000 ;  
NSLog(@&#8221;totalMilliseconds=%llu&#8221;,totalMilliseconds);  
return totalMilliseconds;  
}
  
这样，你就可以得到你想要的13位时间戳，并且从这个时间戳里面获取正确的时间（精确到毫秒哟！）。 
  
本文转自晓龙歌：http://longlinyisheng.lofter.com/post/3ca1cc_59c458a