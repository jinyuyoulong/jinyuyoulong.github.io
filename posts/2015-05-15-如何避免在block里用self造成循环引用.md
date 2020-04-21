---
title: 如何避免在Block里用self造成循环引用
author: fan
type: post
date: 2015-05-15T08:00:00+00:00
url: /如何避免在block里用self造成循环引用/
duoshuo_thread_id:
  - 6278603269921047297
  - 6278603269921047297
categories:
  - iOS

---
<p style="margin-top: 0px; margin-bottom: 0px; padding: 0px; color: rgb(85, 85, 85); font-family: &#39;microsoft yahei&#39;; font-size: 15px; line-height: 35px; white-space: normal;">
  本文原引于<a href="http://blog.csdn.net/zhangao0086/article/details/38273239" target="_blank" title="避免block中self循环引用" rel="noopener noreferrer">Bannings的专栏博客</a>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; padding: 0px; color: rgb(85, 85, 85); font-family: &#39;microsoft yahei&#39;; font-size: 15px; line-height: 35px; white-space: normal;">
  一般来说我们总会在设置Block之后，在合适的时间回调Block，而不希望回调Block的时候Block已经被释放了，所以我们需要对Block进行copy，copy到堆中，以便后用。
</p>

<p style="margin-top: 0px; margin-bottom: 0px; padding: 0px; color: rgb(85, 85, 85); font-family: &#39;microsoft yahei&#39;; font-size: 15px; line-height: 35px; white-space: normal;">
  当一个Block被Copy的时候，如果你在Block里进行了一些调用，那么将会有一个强引用指向这些调用方法的调用者，有两个规则：
</p>

<p style="margin-top: 0px; margin-bottom: 0px; padding: 0px; color: rgb(85, 85, 85); font-family: &#39;microsoft yahei&#39;; font-size: 15px; line-height: 35px; white-space: normal;">
</p>

<ul style="color: rgb(85, 85, 85); font-family: &#39;microsoft yahei&#39;; font-size: 15px; line-height: 35px; white-space: normal;" class=" list-paddingleft-2">
  <li>
    <p>
      如果你是通过引用来访问一个实例变量，那么将强引用至self
    </p>
  </li>
  
  <li>
    <p>
      如果你是通过值来访问一个实例变量，那么将直接强引用至这个“值”变量
    </p>
  </li>
</ul>

苹果官方文档里有两个例子来说明这两种情况：

<img src="http://img.blog.csdn.net/20140729170542000?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvemhhbmdhbzAwODY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" width="605" height="291" alt="" style="border: none;" />

上面第一种情况相当于用self.xxx来访问实例变量，所以强引用指向了self；第二种情况把实例变量变成了本地临时变量，强引用将直接指向这个本地的临时变量。大多数情况下，我们只用处理第一种情况就行了，因为第二种情况虽然会造成循环引用，但是临时变量很快就被释放了，不会造成真正的循环引用。要避免强引用到self的话，用__weak把self重新引用一下就行了，像这样：

<ol start="1" class="dp-objc list-paddingleft-2" style="padding: 5px 0px; border: none; position: relative; list-style-position: initial; list-style-image: initial; color: rgb(92, 92, 92);">
  <li>
    <p>
      <span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">__weak&nbsp;</span><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: rgb(0, 0, 255); background-color: inherit; font-weight: bold;">ViewController</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;*weakSelf&nbsp;=&nbsp;</span><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: rgb(0, 0, 255); background-color: inherit; font-weight: bold;">self</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">; &nbsp;</span></span>
    </p>
  </li>
</ol>