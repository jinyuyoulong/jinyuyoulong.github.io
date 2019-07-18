---
title: MAC系统XAMPP 中 MySQL命令行客户端配置使用
id: 129
categories:
  - other technology其他技术
date: 2015-08-07 23:42:00
tags:
---

**<span style="font-size: 18px;">MySQL客户端</span>**

<span style="font-size: 18px; font-weight: bold;">&nbsp; &nbsp; &nbsp;</span><span style="font-size: 12px;">MySQL安装包里面，在一个名为bin的文件夹，放置了很多工具包，但是使用他们的方式是命令行（ps：最近上瘾了）。</span>

<span style="font-size: 12px;">&nbsp; &nbsp; &nbsp; 在MAC系统，使用命令行的工具可以使用系统自带的Terminal:</span>

<span style="font-size: 12px;">&nbsp; &nbsp; &nbsp;&nbsp;![](http://img.blog.csdn.net/20140616161819640?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvanNfZGFkYQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)</span>

<span style="font-size: 12px;">&nbsp; &nbsp; &nbsp; 顺便在这提一下，笔者使用的php＋mysql环境是MAC版的XAMPP，MySQL的客户端工具就放置在XAMPP里面的bin文件夹。</span>

<span style="font-size: 12px;">&nbsp; &nbsp; &nbsp; 但是如何才能使用这客户端？</span>

<span style="font-size: 12px;">&nbsp; &nbsp; &nbsp; 在Terminal进入到XAMPP的bin文件夹，输入命令：</span><embed id="ZeroClipboardMovie_1" src="http://static.blog.csdn.net/scripts/ZeroClipboard/ZeroClipboard.swf" loop="false" menu="false" quality="best" bgcolor="#ffffff" width="18" height="18" name="ZeroClipboardMovie_1" align="middle" allowscriptaccess="always" allowfullscreen="false" type="application/x-shockwave-flash" pluginspage="http://www.macromedia.com/go/getflashplayer" flashvars="id=1&amp;width=18&amp;height=18" wmode="transparent" style="font-family: sans-serif; font-size: 16px;"/>

1.  <span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">mysql&nbsp;-u&nbsp;root&nbsp;-p&nbsp;&nbsp;</span></span>

<span style="font-size: 12px;">&nbsp; &nbsp; &nbsp; 并没有笔者想要的结果，应该是提示输入密码的呀？？？？？？</span>

<span style="font-size: 12px;">&nbsp; &nbsp; &nbsp; 在Terminal反馈给我的确是 : command not found</span>

<span style="white-space: pre;"></span>what ? 明明就在面前，如何not found，这下苦逼了！好吧，看来需要花点时间找找问题所在了。

<span style="white-space: pre;"></span>经过很长很长很长...............的时间里，终于....

<span style="white-space: pre;"></span>原来当你输入命令的时间，系统会在/usr/bin这个位置里寻找你输入的命令，如果你没有把命令引入到这个位置，无论你直接cd到工具具体的位置调用，也是白费

&nbsp; &nbsp; &nbsp; &nbsp; 功夫的。只要把这个工具的绝对位置引入到/usr/bin，所有的问题就迎刃而解了，只要我们把这条命令执行：

1.  <span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">ln&nbsp;-s&nbsp;/applications/xampp/bin/mysql&nbsp;/usr/bin&nbsp;&nbsp;</span></span>

<span style="white-space: pre;"></span>

<span style="white-space: pre;"></span>这个时候，我们再输入链接数据库命令，然后：

&nbsp; &nbsp; &nbsp; &nbsp;![](http://img.blog.csdn.net/20140616163422578?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvanNfZGFkYQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

<span style="white-space: pre;"></span>