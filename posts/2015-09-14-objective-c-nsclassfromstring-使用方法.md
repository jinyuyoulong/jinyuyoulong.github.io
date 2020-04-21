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
<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  NSClassFromString 是一个很有用的东西，尤其在进行 iPhone toolchain 的开发上。
</p>

<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  正常来说，
</p>

<pre style="margin-top: 0px; margin-bottom: 2.1em; padding: 0.8em 1em; border: 1px solid rgb(5, 35, 43); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.45em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 13px; vertical-align: baseline; box-shadow: rgba(0, 0, 0, 0.0588235) 0px 0px 10px; border-radius: 0.4em; color: rgb(147, 161, 161); overflow: auto; background-image: url(http://cnbin.github.io/images/noise.png?1431911703); background-color: rgb(0, 43, 54); background-position: 0% 0%;" class="brush:java;toolbar:false;">id&nbsp;myObj&nbsp;=&nbsp;[[NSClassFromString(@"MySpecialClass")&nbsp;alloc]&nbsp;init];</pre>

<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  和
</p>

<pre style="margin-top: 0px; margin-bottom: 2.1em; padding: 0.8em 1em; border: 1px solid rgb(5, 35, 43); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.45em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 13px; vertical-align: baseline; box-shadow: rgba(0, 0, 0, 0.0588235) 0px 0px 10px; border-radius: 0.4em; color: rgb(147, 161, 161); overflow: auto; background-image: url(http://cnbin.github.io/images/noise.png?1431911703); background-color: rgb(0, 43, 54); background-position: 0% 0%;" class="brush:cpp;toolbar:false;">id&nbsp;myObj&nbsp;=&nbsp;[[MySpecialClass&nbsp;alloc]&nbsp;init];</pre>

<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  是一样的。但是，如果你的程序中并不存在 MySpecialClass 这个类，下面的写法会出错，而上面的写法只是返回一个空对象而已。
</p>

<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  因此，在某些情况下，可以使用&nbsp;<code style="margin: -1px 0px; padding: 0px 0.3em; border: 1px solid rgb(221, 221, 221); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 0.8em; vertical-align: baseline; display: inline-block; color: rgb(85, 85, 85); border-radius: 0.4em; background: rgb(255, 255, 255);">NSClassFromString</code>&nbsp;来进行你不确定的类的初始化。
</p>

<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  比如在 iPhone 中，NSTask 可能就会出现这种情况，所以在你需要使用 NSTask 时，最好使用：
</p>

<pre style="margin-top: 0px; margin-bottom: 2.1em; padding: 0.8em 1em; border: 1px solid rgb(5, 35, 43); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.45em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 13px; vertical-align: baseline; box-shadow: rgba(0, 0, 0, 0.0588235) 0px 0px 10px; border-radius: 0.4em; color: rgb(147, 161, 161); overflow: auto; background-image: url(http://cnbin.github.io/images/noise.png?1431911703); background-color: rgb(0, 43, 54); background-position: 0% 0%;" class="brush:java;toolbar:false;">[[NSClassFromString(@"NSTask")&nbsp;.....]]</pre>

<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  而不要直接使用&nbsp;<code style="margin: -1px 0px; padding: 0px 0.3em; border: 1px solid rgb(221, 221, 221); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: Menlo, Monaco, &#39;Andale Mono&#39;, &#39;lucida console&#39;, &#39;Courier New&#39;, monospace; font-size: 0.8em; vertical-align: baseline; display: inline-block; color: rgb(85, 85, 85); border-radius: 0.4em; background: rgb(255, 255, 255);">[NSTask ...]</code>&nbsp;这种写法。
</p>

<p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
  NSClassFromString 的好处是：
</p>

<ol style="margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;" class=" list-paddingleft-2">
  <li>
    <p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
      弱化连接，因此并不会把没有的 Framework 也 link 到程序中。
    </p>
  </li>
  
  <li>
    <p style="margin-top: 0px; margin-bottom: 1.5em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 18.4px; vertical-align: baseline;">
      不需要使用 import，因为类是动态加载的，只要存在就可以加载。因此如果你的 toolchain 中没有某个类的头文件定义，而你确信这个类是可以用的，那么也可以用这种方法
    </p>
  </li>
</ol>

<footer style="margin: 2em 0px 0px; padding: 0px 0px 2.5em; border: 0px; font-stretch: inherit; line-height: 27.6px; font-family: 'PT Sans', 'Helvetica Neue', Arial, sans-serif; font-size: 18.4px; vertical-align: baseline; color: rgb(34, 34, 34); white-space: normal; background-color: rgb(248, 248, 248);"> 

<p class="meta" style="margin-top: 0px; margin-bottom: 0.8em; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 0.85em; vertical-align: baseline; clear: both; overflow: hidden;">
  <span class="byline author vcard" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">Posted by&nbsp;<span class="fn" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">陈斌彬</span></span>&nbsp;<time class="entry-date" datetime="2015-07-02T09:30:24+08:00" style=" margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;"><span class="date" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;"><span class="date-month" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">Jul</span>&nbsp;<span class="date-day" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">2</span><span class="date-suffix" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">nd</span>,&nbsp;<span class="date-year" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">2015</span></span>&nbsp;<span class="time" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">9:30 am</span></time>&nbsp;<span class="categories" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline;">&nbsp;<a class="category" href="http://cnbin.github.io/blog/categories/objective-c/" style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 15.64px; vertical-align: baseline; color: rgb(117, 21, 144); transition: color 0.3s; white-space: pre-wrap; word-wrap: break-word;">objective-c</a></span>
</p></footer>