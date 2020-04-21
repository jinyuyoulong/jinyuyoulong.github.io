---
title: UISegmentedControl简单使用
author: fan
type: post
date: 2015-05-14T08:53:26+00:00
url: /uisegmentedcontrol简单使用/
duoshuo_thread_id:
  - 6278603269816189697
  - 6278603269816189697
categories:
  - iOS

---
<p style="margin-top: 0px; margin-bottom: 0px;">
  <span style="font-family: Menlo; color: rgb(185, 134, 10);">NSArray</span><font face="Menlo"> * segMArr = [</font><span style="font-family: Menlo; color: rgb(185, 134, 10);">NSArray</span> <span style="font-family: Menlo; color: rgb(87, 44, 179);">arrayWithObjects</span><font face="Menlo">:</font><span style="color: rgb(195, 195, 0);"><font face="Menlo">@"</font><font face="Heiti SC Light"></font></span><span style="font-family: Menlo; color: rgb(195, 195, 0);">"</span><font face="Menlo">,</font><span style="font-family: Menlo; color: rgb(195, 195, 0);">@"</span><span style="color: rgb(195, 195, 0);"><font face="Heiti SC Light">1</font></span><span style="font-family: Menlo; color: rgb(195, 195, 0);">"</span><font face="Menlo">, </font><span style="font-family: Menlo; color: rgb(6, 54, 152);">nil</span><font face="Menlo">];</font>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(185, 134, 10);">
  UISegmentedControl<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> * segmentC = [[</span>UISegmentedControl<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span><span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">alloc</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">]</span><span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">initWithItems</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">:segMArr];</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; segmentC.<span style="font-variant-ligatures: no-common-ligatures; color: #723eae">frame</span> = <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">CGRectMake</span>(0, <span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">178</span>, <font color="#59351d">320</font>, <span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">30</span>);
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(87, 44, 179);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; segmentC.</span><span style="font-variant-ligatures: no-common-ligatures; color: #723eae">segmentedControlStyle</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> = </span>UISegmentedControlStylePlain<span style="font-variant-ligatures: no-common-ligatures; color: #000000">;</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; segmentC.<span style="font-variant-ligatures: no-common-ligatures; color: #723eae">tintColor</span> = <font color="#59351d">[UIColor BlueColor]</font>;
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(114, 62, 174);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; segmentC.</span>selectedSegmentIndex<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> = </span><span style="font-variant-ligatures: no-common-ligatures; color: #272ad8"></span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">;</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(87, 44, 179);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; [segmentC </span>addTarget<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">self</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>action<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">@selector</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">(segmentedControlSelected:) </span>forControlEvents<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span>UIControlEventValueChanged<span style="font-variant-ligatures: no-common-ligatures; color: #000000">];</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; [bgView <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">addSubview</span>:segmentC];
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &#8211; (<span style="font-variant-ligatures: no-common-ligatures; color: #063698">void</span>)segmentedControlSelected:(<span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">UISegmentedControl</span>*)seg{
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(114, 62, 174);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; </span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">if</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> (seg.</span>selectedSegmentIndex<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> == </span><span style="font-variant-ligatures: no-common-ligatures; color: #272ad8"></span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">) {</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; min-height: 19px;">
  &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(114, 62, 174);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; }</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">else</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">if</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> (seg.</span>selectedSegmentIndex<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> == </span><span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">1</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">){</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; min-height: 19px;">
  &nbsp;&nbsp; &nbsp;
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; }
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  }
</p>