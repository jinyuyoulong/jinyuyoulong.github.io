---
title: Objective-c NSClassFromString 使用方法
categories: [iOS]
date: 2015-09-14 11:58:58
---

NSClassFromString 是一个很有用的东西，尤其在进行 iPhone toolchain 的开发上。

正常来说，
<pre style="margin-top: 0px; margin-bottom: 2.1em; padding: 0.8em 1em; border: 1px solid rgb(5, 35, 43); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.45em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 13px; vertical-align: baseline; box-shadow: rgba(0, 0, 0, 0.0588235) 0px 0px 10px; border-radius: 0.4em; color: rgb(147, 161, 161); overflow: auto; background-image: url(http://cnbin.github.io/images/noise.png?1431911703); background-color: rgb(0, 43, 54); background-position: 0% 0%;" class="brush:java;toolbar:false;">id&nbsp;myObj&nbsp;=&nbsp;[[NSClassFromString(@&quot;MySpecialClass&quot;)&nbsp;alloc]&nbsp;init];</pre>

和
<pre style="margin-top: 0px; margin-bottom: 2.1em; padding: 0.8em 1em; border: 1px solid rgb(5, 35, 43); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.45em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 13px; vertical-align: baseline; box-shadow: rgba(0, 0, 0, 0.0588235) 0px 0px 10px; border-radius: 0.4em; color: rgb(147, 161, 161); overflow: auto; background-image: url(http://cnbin.github.io/images/noise.png?1431911703); background-color: rgb(0, 43, 54); background-position: 0% 0%;" class="brush:cpp;toolbar:false;">id&nbsp;myObj&nbsp;=&nbsp;[[MySpecialClass&nbsp;alloc]&nbsp;init];</pre>

是一样的。但是，如果你的程序中并不存在 MySpecialClass 这个类，下面的写法会出错，而上面的写法只是返回一个空对象而已。

因此，在某些情况下，可以使用&nbsp;`NSClassFromString`&nbsp;来进行你不确定的类的初始化。

比如在 iPhone 中，NSTask 可能就会出现这种情况，所以在你需要使用 NSTask 时，最好使用：
<pre style="margin-top: 0px; margin-bottom: 2.1em; padding: 0.8em 1em; border: 1px solid rgb(5, 35, 43); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.45em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 13px; vertical-align: baseline; box-shadow: rgba(0, 0, 0, 0.0588235) 0px 0px 10px; border-radius: 0.4em; color: rgb(147, 161, 161); overflow: auto; background-image: url(http://cnbin.github.io/images/noise.png?1431911703); background-color: rgb(0, 43, 54); background-position: 0% 0%;" class="brush:java;toolbar:false;">[[NSClassFromString(@&quot;NSTask&quot;)&nbsp;.....]]</pre>

而不要直接使用&nbsp;`[NSTask ...]`&nbsp;这种写法。

NSClassFromString 的好处是：

1.  弱化连接，因此并不会把没有的 Framework 也 link 到程序中。

2.  不需要使用 import，因为类是动态加载的，只要存在就可以加载。因此如果你的 toolchain 中没有某个类的头文件定义，而你确信这个类是可以用的，那么也可以用这种方法

<footer style="margin: 2em 0px 0px; padding: 0px 0px 2.5em; border: 0px; font-stretch: inherit; line-height: 27.6px; font-family: &#39;PT Sans&#39;, &#39;Helvetica Neue&#39;, Arial, sans-serif; font-size: 18.4px; vertical-align: baseline; color: rgb(34, 34, 34); white-space: normal; background-color: rgb(248, 248, 248);">

<span class="byline author vcard" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">Posted by&nbsp;<span class="fn" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">陈斌彬</span></span>&nbsp;<time class="entry-date" datetime="2015-07-02T09:30:24+08:00" style="

margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;"><span class="date" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;"><span class="date-month" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">Jul</span>&nbsp;<span class="date-day" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">2</span><span class="date-suffix" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">nd</span>,&nbsp;<span class="date-year" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">2015</span></span>&nbsp;<span class="time" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">9:30 am</span></time>&nbsp;<span class="categories" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">&nbsp;[objective-c](http://cnbin.github.io/blog/categories/objective-c/)</span>
</footer>