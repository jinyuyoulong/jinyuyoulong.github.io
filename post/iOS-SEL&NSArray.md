---
title: SEL如何保存到NSArray数组中
categories: [iOS]
date: 2015-11-04 11:09:43
tags:
---

首先，SEL是不可以保存到array数组中去的。

其次，SEL有两种创建方法：
<pre class="brush:cpp;toolbar:false">SEL&nbsp;s1&nbsp;=&nbsp;&nbsp;@selector&nbsp;(test1);&nbsp;&nbsp;&nbsp;//&nbsp;将test1方法转换为NSString对象
SEL&nbsp;s2&nbsp;=&nbsp;NSSelectorFromString&nbsp;(&nbsp;@&quot;test1&quot;&nbsp;);&nbsp;&nbsp;&nbsp;//&nbsp;将一个字符串&nbsp;&nbsp;方法&nbsp;转换成为SEL对象</pre>

NSArray无法保存SEL，但是可以保存NSString。

所以我们利用第二种创建方法，讲SEL的方法名以字符串的方式保存到NSArray数组中即可。

举个栗子：
<pre class="brush:cpp;toolbar:false">NSArray&nbsp;*&nbsp;selArr&nbsp;=&nbsp;@[@&quot;gotoSelectCity&quot;,&nbsp;@&quot;gotoSelectTitle&quot;];
UITapGestureRecognizer&nbsp;*&nbsp;rightLabelGest&nbsp;=&nbsp;[[UITapGestureRecognizer&nbsp;alloc]initWithTarget:self&nbsp;action:NSSelectorFromString(selArr[i])];</pre>

<span style="font-variant-ligatures: no-common-ligatures; color: #e7cf81"></span>