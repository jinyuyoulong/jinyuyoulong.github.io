---
title: svn上传.a文件
categories: [iOS]
date: 2015-04-23 09:46:53
tags:
---

<span style="color: rgb(51, 51, 51); font-size: 14px; font-family: &#39;Hiragino Sans GB W3&#39;, &#39;Hiragino Sans GB&#39;, Arial, Helvetica, simsun, u5b8bu4f53; line-height: 24.5px;">在mac下很多svn管理工具默认都不能上传.a文件，这让人很苦恼。从网上扒了下，找到了两个方法。</span>
<span style="color: rgb(51, 51, 51); font-size: 14px; line-height: 24.5px; font-family: &#39;Hiragino Sans GB W3&#39;, &#39;Hiragino Sans GB&#39;, Arial, Helvetica, simsun, u5b8bu4f53;">方法一：
打开终端，cd 进入到需要上传的.a文件所在的文件夹。&nbsp;确保 ls能看到.a文件
然后使用命令，如：svn add libzbar.a
使用完成后出现
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;A &nbsp;(bin) &nbsp;libzbar.a
</span><span style="color: rgb(51, 51, 51); font-family: Arial; font-size: 14px; line-height: 26px; background-color: rgb(255, 255, 255);"></span>

<span style="line-height: 24.5px; font-family: &#39;Hiragino Sans GB W3&#39;, &#39;Hiragino Sans GB&#39;, Arial, Helvetica, simsun, u5b8bu4f53;">表示添加成功，用svn图形管理工具就可以看到，刚才添加的.a文件，此时就可以手动上传了。</span>

<span style="line-height: 24.5px; font-family: &#39;Hiragino Sans GB W3&#39;, &#39;Hiragino Sans GB&#39;, Arial, Helvetica, simsun, u5b8bu4f53;">再次update后commit后 .a 文件就传成功了</span>

<span style="line-height: 24.5px; font-family: &#39;Hiragino Sans GB W3&#39;, &#39;Hiragino Sans GB&#39;, Arial, Helvetica, simsun, u5b8bu4f53;">
</span>

<span style="line-height: 24.5px; font-family: &#39;Hiragino Sans GB W3&#39;, &#39;Hiragino Sans GB&#39;, Arial, Helvetica, simsun, u5b8bu4f53;">方法二：</span>

通过终端打开配置文件: open ~/.subversion/config

<span style="line-height: 24.5px; font-family: &#39;Hiragino Sans GB W3&#39;, &#39;Hiragino Sans GB&#39;, Arial, Helvetica, simsun, u5b8bu4f53;"></span>

把下面两行(也可能是一行)中的注释和*.a去掉,&nbsp;<span style="font-family: Arial, Helvetica, simsun, u5b8bu4f53; line-height: 21px; background-color: rgb(247, 252, 255);">默认为注释掉了的，这表示SVN已经将它们作为默认值了。</span>

（取消注释估计是把#去掉，个人猜测未验证）好吧，其实我没有看明白如何取消注释![大哭](http://static.blog.csdn.net/xheditor/xheditor_emot/default/wail.gif)

# global-ignores = *.o *.lo *.la *.al .libs *.so *.so.[0-9]* *.pyc *.pyo
# &nbsp; *.rej *~ #*# .#* .*.swp .DS_Store

注意：去掉#号后要顶行

然后保存.

说明：本文获得[佘小兔的日志](http://yul100887.blog.163.com/blog/static/20033613520121117105938991/)（方法一）和&nbsp;[如何往svn上传原本被忽略的*.a文件](http://blog.csdn.net/xu_yunan/article/details/6728216)（方法二）的帮助

在此感谢所有分享知识的朋友们。