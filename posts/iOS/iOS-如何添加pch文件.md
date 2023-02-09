---
title: Xcode如何添加pch文件
author: fan
type: post
date: 2015-07-14T03:31:06+00:00
url: /如何添加pch文件/
duoshuo_thread_id:
  - 6278603271414219521
  - 6278603271414219521
categories:
  - iOS

---
Xcode6.0之后去掉了Precompile Prefix Header 文件，<span style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; line-height: 27.200000762939453px; text-indent: 1em;">主要原因可能在于Prefix Header大大的增加了Build的时间。没有了Prefix Header之后就要通过手动@import来手动导入头文件了，在失去了编程便利性的同时也降低了Build的时间。具体原因</span>

<p style="margin-top: 0px; margin-bottom: 0.75em; line-height: 27.200000762939453px; text-indent: 1em; color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; white-space: normal;">
  StackOverFlow上讨论的已经比较清晰了
</p>

<p style="margin-top: 0px; margin-bottom: 0.75em; line-height: 27.200000762939453px; text-indent: 1em; color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; white-space: normal;">
  <a style="color: #949494; text-decoration: none; transition: 0.25s; -webkit-transition: 0.25s; border-bottom-width: 1px; border-bottom-style: dashed; border-bottom-color: #949494; font-style: italic; font-weight: bold;" href="http://stackoverflow.com/questions/24158648/why-isnt-projectname-prefix-pch-created-automatically-in-xcode-6" target="_blank" rel="nofollow,noindex noopener noreferrer">StackOverFlow:为什么xcode6没有自动创建pch文件呢？</a>
</p>

<h3 style="margin: 0px 0px 0.5em; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; line-height: 20px; color: #333333; text-rendering: optimizelegibility; font-size: 18px; text-indent: 1em; white-space: normal;">
  那么如何在Xcode6中添加pch（Precompile Prefix Header）？
</h3>

<p style="margin-top: 0px; margin-bottom: 0.75em; line-height: 27.200000762939453px; text-indent: 1em; color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; white-space: normal;">
  1，Command+N，打开新建文件窗口：ios->other->PCH file，创建一个pch文件：“工程名-Prefix.pch”
</p>

<span style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; line-height: 27.200000762939453px; text-indent: 16px; background-color: #fefefe;">    2，将building setting中的precompile header选项的路径添加“$(SRCROOT)/项目名称/pch文件名”（例如：$(SRCROOT)/LotteryFive/LotteryFive-Prefix.pch）,</span><span style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, Arial, STXihei, 'Microsoft YaHei', 微软雅黑, sans-serif; line-height: 27.200000762939453px; text-indent: 1em;">编译一下程序，如果有错误检查一下添加的路径是否正确。</span>
  
<
  
p style=&#8221;margin-top: 0px; margin-bottom: 0.75em; line-height: 27.200000762939453px; text-indent: 1em; color: rgb(51, 51, 51); font-family: &#8216;Helvetica Neue&#8217;, Helvetica, Tahoma, Arial, STXihei, &#8216;Microsoft YaHei&#8217;, 微软雅黑, sans-serif; white-space: normal;&#8221;>3，将Precompile Prefix Header为YES，预编译后的pch文件会被缓存起来，可以提高编译速度
  
&nbsp;
  
<figure id="attachment_403" aria-describedby="caption-attachment-403" style="width: 600px" class="wp-caption alignleft"><a href="http://blog-fansrss.rhcloud.com/wp-content/uploads/2015/07/PCH文件.png" rel="attachment wp-att-403"><img class="size-large wp-image-403" src="http://fanjinlong.xyz/wp-content/uploads/2016/04/PCH文件-1024x475.png" alt="pch文件build settings" width="600" height="278" /></a><figcaption id="caption-attachment-403" class="wp-caption-text">pch文件build settings</figcaption></figure>