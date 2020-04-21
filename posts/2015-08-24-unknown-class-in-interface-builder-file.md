---
title: 'Unknown Class **** in Interface Builder file'
author: fan
type: post
date: 2015-08-24T02:44:12+00:00
url: /unknown-class-in-interface-builder-file/
duoshuo_thread_id:
  - 6278603325873062658
  - 6278603325873062658
views:
  - 10
  - 10
categories:
  - iOS

---
<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  I added a UIView xib file using the root class of&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, &#39;Lucida Console&#39;, &#39;Liberation Mono&#39;, &#39;DejaVu Sans Mono&#39;, &#39;Bitstream Vera Sans Mono&#39;, &#39;Courier New&#39;, monospace, sans-serif; white-space: pre-wrap; background-color: rgb(238, 238, 238);">MyView</code>.
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  I created it in the wrong place and so moved it in the project. Same project just a different folder/group.
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  I then had a problem when running saying&#8230;
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  <code style="margin: 0px; padding: 1px 5px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, &#39;Lucida Console&#39;, &#39;Liberation Mono&#39;, &#39;DejaVu Sans Mono&#39;, &#39;Bitstream Vera Sans Mono&#39;, &#39;Courier New&#39;, monospace, sans-serif; white-space: pre-wrap; background-color: rgb(238, 238, 238);">Unknown Class MyView in Interface Builder file</code>
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  I couldn't work out what was wrong so I have now deleted the files both from the project and from the directory.
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  I've done a search using SublimeText2 for the string "MyView" and it doesn't exist anywhere in the project.
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  I've reset the simulator, cleaned the project and the build folder and deleted derived data.
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; clear: both; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  Still getting the same error.
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  Any ideas what I can do now?
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  范子遇到的问题也是这样的，这个问题的产生过程一模一样：
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  开始建了一个xib后来发现设计不行，就有删除了，啊啊啊，从此噩梦开始了。。。
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  只要一运行就崩溃，清楚缓存，不行，删除项目，不行；后来看到据说这是Xcode5的一个bug，但是大哥，我的Xcode版本是6啊，怎么还不解决！只能使用真机测试没问题，也就只能这样了。如此过了几日。
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  但是机智的我会被这点小困难打倒吗，终于有一天我决定解决这个问题（其实是因为，忘带数据线，没办法真机测试了*——*），于是到处Google，哈哈，功夫不负有心人，我从一篇答案中获得了灵感，触类旁通，忽然想到，我的ViewController当初常见的时候使用的是init方法，虽然一般系统默认调用init方法会检查有无nib有的话会调用nib但是希望不能寄托在Xcode身上，我断定就是这里出了问题，于是返回代码试验，将init方法改为initWithNibName方法，command+R 运行OK，
</p>

<p style="margin-top: 0px; margin-bottom: 1em; white-space: normal; padding: 0px; border: 0px; font-size: 15px; color: rgb(34, 34, 34); font-family: &#39;Helvetica Neue&#39;, Helvetica, Arial, sans-serif; line-height: 19.5px; background-color: rgb(255, 255, 255);">
  至此问题解决，噢耶！
</p>