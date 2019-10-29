---
title: Unknown Class **** in Interface Builder file
categories: [iOS]
date: 2015-08-24 10:44:12
---

I added a UIView xib file using the root class of&nbsp;`MyView`.

I created it in the wrong place and so moved it in the project. Same project just a different folder/group.

I then had a problem when running saying...

`Unknown Class MyView in Interface Builder file`

I couldn&#39;t work out what was wrong so I have now deleted the files both from the project and from the directory.

I&#39;ve done a search using SublimeText2 for the string &quot;MyView&quot; and it doesn&#39;t exist anywhere in the project.

I&#39;ve reset the simulator, cleaned the project and the build folder and deleted derived data.

Still getting the same error.

Any ideas what I can do now?

范子遇到的问题也是这样的，这个问题的产生过程一模一样：

开始建了一个xib后来发现设计不行，就有删除了，啊啊啊，从此噩梦开始了。。。

只要一运行就崩溃，清楚缓存，不行，删除项目，不行；后来看到据说这是Xcode5的一个bug，但是大哥，我的Xcode版本是6啊，怎么还不解决！只能使用真机测试没问题，也就只能这样了。如此过了几日。

但是机智的我会被这点小困难打倒吗，终于有一天我决定解决这个问题（其实是因为，忘带数据线，没办法真机测试了*——*），于是到处Google，哈哈，功夫不负有心人，我从一篇答案中获得了灵感，触类旁通，忽然想到，我的ViewController当初常见的时候使用的是init方法，虽然一般系统默认调用init方法会检查有无nib有的话会调用nib但是希望不能寄托在Xcode身上，我断定就是这里出了问题，于是返回代码试验，将init方法改为initWithNibName方法，command+R 运行OK，

至此问题解决，噢耶！