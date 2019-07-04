---
title: UISegmentedControl简单使用
id: 59
categories:
  - iOS
date: 2015-05-14 16:53:26
tags:
---

<span style="font-family: Menlo; color: rgb(185, 134, 10);">NSArray</span><font face="Menlo"> * segMArr = [</font><span style="font-family: Menlo; color: rgb(185, 134, 10);">NSArray</span> <span style="font-family: Menlo; color: rgb(87, 44, 179);">arrayWithObjects</span><font face="Menlo">:</font><span style="color: rgb(195, 195, 0);"><font face="Menlo">@&quot;</font><font face="Heiti SC Light">0</font></span><span style="font-family: Menlo; color: rgb(195, 195, 0);">&quot;</span><font face="Menlo">,</font><span style="font-family: Menlo; color: rgb(195, 195, 0);">@&quot;</span><span style="color: rgb(195, 195, 0);"><font face="Heiti SC Light">1</font></span><span style="font-family: Menlo; color: rgb(195, 195, 0);">&quot;</span><font face="Menlo">, </font><span style="font-family: Menlo; color: rgb(6, 54, 152);">nil</span><font face="Menlo">];</font>

UISegmentedControl<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> * segmentC = [[</span>UISegmentedControl<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span><span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">alloc</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">]</span><span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">initWithItems</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">:segMArr];</span>

&nbsp; &nbsp; segmentC.<span style="font-variant-ligatures: no-common-ligatures; color: #723eae">frame</span> = <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">CGRectMake</span>(0, <span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">178</span>, <font color="#59351d">320</font>, <span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">30</span>);

<span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; segmentC.</span><span style="font-variant-ligatures: no-common-ligatures; color: #723eae">segmentedControlStyle</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> = </span>UISegmentedControlStylePlain<span style="font-variant-ligatures: no-common-ligatures; color: #000000">;</span>

&nbsp; &nbsp; segmentC.<span style="font-variant-ligatures: no-common-ligatures; color: #723eae">tintColor</span> = <font color="#59351d">[UIColor BlueColor]</font>;

<span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; segmentC.</span>selectedSegmentIndex<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> = </span><span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">0</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">;</span>

<span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; [segmentC </span>addTarget<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">self</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>action<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">@selector</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">(segmentedControlSelected:) </span>forControlEvents<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span>UIControlEventValueChanged<span style="font-variant-ligatures: no-common-ligatures; color: #000000">];</span>

&nbsp; &nbsp; [bgView <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">addSubview</span>:segmentC];

- (<span style="font-variant-ligatures: no-common-ligatures; color: #063698">void</span>)segmentedControlSelected:(<span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">UISegmentedControl</span>*)seg{

<span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; </span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">if</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> (seg.</span>selectedSegmentIndex<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> == </span><span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">0</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">) {</span>

&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;

<span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; }</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">else</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">if</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> (seg.</span>selectedSegmentIndex<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> == </span><span style="font-variant-ligatures: no-common-ligatures; color: #272ad8">1</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">){</span>

&nbsp;&nbsp; &nbsp;

&nbsp; &nbsp; }

}