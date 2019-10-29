---
title: NSString 位数不足补0
categories: [iOS]
date: 2016-01-15 16:22:44
---

%0nd ，n是多少位。0表示补0

<div>如果是%nd，就是不满n位，自动补充空格。</div>

<span class="s1">   NSString</span><span class="s2"> * testStr;</span>

<span class="s3"><span class="Apple-converted-space">    </span></span><span class="s4">int</span><span class="s3"> f = </span><span class="s5">12</span><span class="s3">;</span>

<span class="s2"><span class="Apple-converted-space">    </span>testStr = [</span><span class="s3">NSString</span> <span class="s3">stringWithFormat</span><span class="s2">:</span><span class="s6">@"%03d"</span><span class="s2">,f];</span>

<span class="s3"><span class="Apple-converted-space">    </span></span><span class="s1">NSLog</span><span class="s3">(</span><span class="s6">@"%@"</span><span class="s3">,testStr);</span>