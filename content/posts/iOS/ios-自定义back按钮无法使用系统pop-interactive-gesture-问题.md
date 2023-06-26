---
title: 自定义back按钮无法使用系统pop interactive gesture 问题
author: fan
type: post
date: 2015-08-06T10:50:01+00:00
url: /自定义back按钮无法使用系统pop-interactive-gesture-问题/
duoshuo_thread_id:
  - 6278603297330823938
  - 6278603297330823938
categories:
  - iOS

---
两种解决办法：

方法一：

<p style="margin-top: 0px; margin-bottom: 0.75em; padding: 0px; white-space: normal; line-height: 28.7999992370605px; color: rgb(51, 51, 51); font-family: &#39;Helvetica Neue&#39;, Helvetica, Tahoma, Arial, STXihei, &#39;Microsoft YaHei&#39;, 微软雅黑, sans-serif;">
  A，我的应用是自定义的返回按钮图标(默认返回按钮样式不会出现问题3)，为了保险，写了这句代码[self.navigationItem setHidesBackButton:YES]。 由于自定义返回按钮，所以iOS7自带返回手势无效。在需要的页面加上navigationController.interactivePopGestureRecognizer.delegate = self 返回手势好用了。
</p>

<p style="margin-top: 0px; margin-bottom: 0.75em; padding: 0px; white-space: normal; line-height: 28.7999992370605px; color: rgb(51, 51, 51); font-family: &#39;Helvetica Neue&#39;, Helvetica, Tahoma, Arial, STXihei, &#39;Microsoft YaHei&#39;, 微软雅黑, sans-serif;">
  B，于是出现了第二个问题。 在一级视图中，iOS样式返回的手势滑动一下，然后进入二级视图，发现，画面卡住了，按Home键转入后台，再返回应用，发现并没有Crash掉，而是直 接跳到了二级视图里，运行正常了，大家知道push和pop的原理是用进栈出栈完成的，可能因为在一级视图中滑动那一下，影响了视图在栈中的位置。 好，先解决一下这个问题，一级视图中一定要加入self.navigationController.interactivePopGestureRecognizer.enabled = NO;，先把iOS7手势返回屏蔽掉，到二级视图再用self.navigationController.interactivePopGestureRecognizer.enabled = YES打开。就Ok了。
</p>

<p style="margin-top: 0px; margin-bottom: 0.75em; padding: 0px; white-space: normal; line-height: 28.7999992370605px; color: rgb(51, 51, 51); font-family: &#39;Helvetica Neue&#39;, Helvetica, Tahoma, Arial, STXihei, &#39;Microsoft YaHei&#39;, 微软雅黑, sans-serif;">
  C，好，第三个问题相继出现（其实是跟第二个一起出来的）。 手势返回拖动一半，放手，navigationBar上会出现三个小蓝点，而且位置不规律，可以肯定这个不是项目代码或者图片搞出来的东西，一定是SDK自己蹦出來的。 后台尝试发现UIBarButtonItem的title如果是nil的话，就会有这个问题。 解决方案：把[self.navigationItem setHidesBackButton:YES];去掉，然後把假装成返回按钮的UIBarButtonItem的title设置成@""。
</p>

<p style="margin-top: 0px; margin-bottom: 0.75em; padding: 0px; white-space: normal; line-height: 28.7999992370605px; color: rgb(51, 51, 51); font-family: &#39;Helvetica Neue&#39;, Helvetica, Tahoma, Arial, STXihei, &#39;Microsoft YaHei&#39;, 微软雅黑, sans-serif;">
</p>

<p style="margin-top: 0px; margin-bottom: 0.75em; padding: 0px; white-space: normal; line-height: 28.7999992370605px; color: rgb(51, 51, 51); font-family: &#39;Helvetica Neue&#39;, Helvetica, Tahoma, Arial, STXihei, &#39;Microsoft YaHei&#39;, 微软雅黑, sans-serif;">
  方法二：
</p>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;&nbsp;&lt;&nbsp;&nbsp;&nbsp;&gt;</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;-&nbsp;(&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.interactivePopGestureRecognizer.&nbsp;=&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.&nbsp;=</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;"><br /> <span style="margin: 0px; padding: 0px; line-height: 1.5 !important;"> &nbsp; &nbsp;[super dealloc];<br /> &nbsp; &nbsp;<br /></span> <span style="margin: 0px; padding: 0px; line-height: 1.5 !important;">}<br /><br /></span>&nbsp;</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;&nbsp;mark&nbsp;-&nbsp;View&nbsp;lifecycle</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;-&nbsp;(&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.interactivePopGestureRecognizer.&nbsp;=&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.&nbsp;=&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;(</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;&nbsp;mark&nbsp;-&nbsp;Override</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;-&nbsp;()pushViewController:(UIViewController&nbsp;*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.interactivePopGestureRecognizer.enabled&nbsp;=&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mark&nbsp;-&nbsp;UINavigationControllerDelegate</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;&nbsp;-&nbsp;()navigationController:(UINavigationController&nbsp;*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;didShowViewController:(UIViewController&nbsp;*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;navigationController.interactivePopGestureRecognizer.enabled&nbsp;=</pre>

<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;"><font color="#008080"><span style="line-height: 24px;"><br /></span></font> <span style="margin: 0px; padding: 0px; color: rgb(0, 0, 255); line-height: 1.5 !important;">@end</span></pre>



<p style="font-size: 14px; white-space: normal; margin: 10px auto; padding-top: 0px; padding-bottom: 0px; line-height: 18px; color: rgb(68, 68, 68); font-family: tahoma, arial, sans-serif;">
  &nbsp;
</p>

<p style="font-size: 14px; white-space: normal; margin: 10px auto; padding-top: 0px; padding-bottom: 0px; line-height: 18px; color: rgb(68, 68, 68); font-family: tahoma, arial, sans-serif;">
  3、Pop interactive gesture冲突，造成页面假死问题
</p>

<p style="font-size: 14px; white-space: normal; margin: 10px auto 10px 30px; padding-top: 0px; padding-bottom: 0px; line-height: 18px; color: rgb(68, 68, 68); font-family: tahoma, arial, sans-serif;">
  我遇到的情况是，Push/Pop页面时，没有立即得到想要的效果，页面没有显出出来，NavigationController的didShowViewController:回调方法也没有调用。
</p>

<p style="font-size: 14px; white-space: normal; margin: 10px auto 10px 30px; padding-top: 0px; padding-bottom: 0px; line-height: 18px; color: rgb(68, 68, 68); font-family: tahoma, arial, sans-serif;">
  页面布局情况是这样的：视图A，有一个Pan手势；视图B是TabBarController，其ViewControllers都是NavigationController。视图B是视图A的子视图。
</p>

<p style="font-size: 14px; white-space: normal; margin: 10px auto 10px 30px; padding-top: 0px; padding-bottom: 0px; line-height: 18px; color: rgb(68, 68, 68); font-family: tahoma, arial, sans-serif;">
  后来找到原因是：navigationController的interactive pop手势与视图A的pan手势冲突。
</p>

<p style="font-size: 14px; white-space: normal; margin: 10px auto 10px 30px; padding-top: 0px; padding-bottom: 0px; line-height: 18px; color: rgb(68, 68, 68); font-family: tahoma, arial, sans-serif;">
  具体原因是：rootViewController加载时，调用了didShowViewController:，设置interactivePopGestureRecognizer可用，其实我们并不需要在root的时候也触发这个手势。所以稍加优化如下：
</p>



<pre style="white-space: pre-wrap; word-wrap: break-word; margin-top: 0px; margin-bottom: 0px; padding: 0px; font-family: &#39;Courier New&#39; !important;">&nbsp;-&nbsp;()navigationController:(UINavigationController&nbsp;*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;didShowViewController:(UIViewController&nbsp;*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;([navigationController.viewControllers&nbsp;count]&nbsp;==&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;navigationController.interactivePopGestureRecognizer.enabled&nbsp;=&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;navigationController.interactivePopGestureRecognizer.enabled&nbsp;=&nbsp;&nbsp;&nbsp;}</pre>

<p style="margin-top: 0px; margin-bottom: 0.75em; padding: 0px; white-space: normal; line-height: 28.7999992370605px; color: rgb(51, 51, 51); font-family: &#39;Helvetica Neue&#39;, Helvetica, Tahoma, Arial, STXihei, &#39;Microsoft YaHei&#39;, 微软雅黑, sans-serif;">
</p>