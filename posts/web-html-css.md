---
title: HTML&CSS
tags: [css,html]
categories: [Web]
date: 2015-10-25 17:48:49
---

&lt;p&gt; paragragh 段落

&lt;em&gt; emphasize 强调(显示为斜体)

&lt;span&gt; 样式

&lt;q&gt; quote [kwot] 引用，引号(显示默认添加双引号，故不用再次添加“ ”)

&lt;blockquote&gt; 引用块 ，长文本引用(显示默认为缩进，左右都缩进)

&lt;br /&gt; break 换行 &amp;nbsp; 空格占位符

&lt;hr /&gt; horizontal rule 水平分割线

&lt;address&gt; 地址标签(默认显示为斜体)

&lt;code&gt; 一行代码

&lt;pre&gt; predefined 预定义，多行代码,预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体.

&lt;ul&gt; unordered list 定义无序列表 (前方显示一个小圆点)

&lt;li&gt; list 列表

&lt;ol&gt; orderly list 定义有序列表 (前方显示123等数字)

创建表格的四个元素：table、tbody、tr、th、td

&lt;tbody&gt; table body 表格体

&lt;tr&gt; table row 表格，行

&lt;td&gt; table data 表格数据

&lt;th&gt; table head 表格头

&lt;caption&gt; 表格标题

&lt;table summary=&quot;表格简介文本&quot;&gt;

<span style="font-family:&#39;Helvetica Neue&#39;;font-size:14px;"></span><span style="font-family:&#39;Helvetica Neue&#39;;font-size:14px;"></span>

<span style="color: rgb(99, 87, 82);">&lt;a&gt;&nbsp;action&nbsp;目标&nbsp;，添加超链接&nbsp;例:&nbsp;&lt;a&nbsp;href=&quot;目标网址&quot;&nbsp;title=&quot;鼠标滑过显示的文本&quot;&gt;链接显示的文本&lt;/a&gt;</span>

<span style="color: rgb(99, 87, 82);">
</span>

<span style="color: rgb(99, 87, 82); background-color: rgb(255, 252, 247);">&nbsp;rel&nbsp;属性用于指定当前文档与被链接文档的关系&nbsp;relative&nbsp;相对关系</span>

<span style="color: rgb(99, 87, 82);">&lt;span&nbsp;id=&quot;setGreen&quot;&gt;公开课&lt;/span&gt;</span>

#setGreen{

&nbsp; &nbsp;color:green;

}

<span style="color: rgb(99, 87, 82);">CSS&nbsp;id选择器</span>

<span style="color: rgb(99, 87, 82);">.类选器名称{css样式代码;}</span>

<span style="color: rgb(99, 87, 82);">注意：</span>

1、英文圆点开头

2、其中类选器名称可以任意起名

&lt;span&nbsp;id=&quot;setGreen&quot;&gt;公开课&lt;/span&gt;&nbsp;

<span style="color: rgb(99, 87, 82);">
</span>

<span style="color: rgb(99, 87, 82); white-space: pre-wrap; background-color: rgb(255, 252, 247);">.food&gt;li{border:1px&nbsp;solid&nbsp;red;}</span> <span style="color: rgb(99, 87, 82); background-color: rgb(255, 252, 247);">大于符号(&gt;),用于选择指定标签元素的第一代子元素。</span>

<span style="color: rgb(99, 87, 82); background-color: rgb(255, 252, 247);">solid：表示单线</span>

<span style="color: rgb(99, 87, 82); background-color: rgb(255, 252, 247);">
</span>

<span style="color: rgb(99, 87, 82);">包含选择器，即加入空格,用于选择指定标签元素下的后辈元素。如右侧代码编辑器中的代码：</span>

<span style="color: rgb(99, 87, 82);">.first&nbsp; span{color:red;}</span>

<span style="color: rgb(99, 87, 82);">
</span>

<span style="color: rgb(99, 87, 82);">伪类选择符，它允许给html不存在的标签（标签的某种状态）设置样式&nbsp;:a:hover{color:red;}</span>

上面一行代码就是为&nbsp;a&nbsp;标签鼠标滑过的状态设置字体颜色变红。

<span style="font-size: 17px;"><span style="font-family: Helvetica, &#39;Microsoft Yahei&#39;, ST-Heiti, &#39;Apple Color Emoji&#39;;"><span style="color: rgb(99, 87, 82);">分组选择符：h1,span{color:red;}</span></span></span>

<span style="font-size: 17px;"><span style="font-family: Helvetica, &#39;Microsoft Yahei&#39;, ST-Heiti, &#39;Apple Color Emoji&#39;;"><span style="color: rgb(99, 87, 82);">它相当于下面两行代码：</span></span></span>

h1{color:red;}&nbsp;span{color:red;}