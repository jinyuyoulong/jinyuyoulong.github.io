---
title: 文字上添加删除线
id: 177
categories:
  - iOS
date: 2015-08-21 17:10:49
tags:
---

![](http://images.cnitblog.com/blog/685490/201412/221956443439449.png)

&nbsp; &nbsp;&nbsp;NSString * str = @&quot;ABCDEFG HIJKLMN&quot;;

&nbsp; &nbsp; UILabel * aLab = [[UILabel alloc]initWithFrame:CGRectMake(10, 100, 300, 300)];

<span style="margin: 0px; padding: 0px; line-height: 1.5;">&nbsp; &nbsp; aLab.text = str;</span>

<span style="margin: 0px; padding: 0px; line-height: 1.5;">&nbsp; &nbsp; NSMutableAttributedString * testAttriString = [[NSMutableAttributedString alloc] initWithString:str];</span>

&nbsp;&nbsp; [testAttriString addAttribute:NSStrikethroughStyleAttributeName value:[NSNumber numberWithInt:NSUnderlineStyleSingle] range:NSMakeRange(0, testAttriString.length)];

<span style="margin: 0px; padding: 0px; line-height: 1.5;">&nbsp; &nbsp; aLab.attributedText = testAttriString;</span>

<span style="margin: 0px; padding: 0px; line-height: 1.5;">&nbsp; &nbsp; [self.view addSubview:aLab];</span>