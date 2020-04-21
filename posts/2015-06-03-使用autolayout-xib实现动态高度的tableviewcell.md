---
title: 使用Autolayout xib实现动态高度的TableViewCell
author: fan
type: post
date: 2015-06-03T07:27:18+00:00
url: /使用autolayout-xib实现动态高度的tableviewcell/
duoshuo_thread_id:
  - 6278603269988156162
  - 6278603269988156162
categories:
  - iOS

---
文章来源于<a href="http://itony.me/381.html" target="_blank" rel="noopener noreferrer">http://itony.me/381.html</a>

<h2 style="margin: 40px 0px 15px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-weight: lighter; font-size: 1.6em; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; clear: both; color: rgb(51, 51, 50); letter-spacing: -1px; line-height: 1; -webkit-hyphens: none; word-wrap: break-word; white-space: normal;">
  创建Xib文件
</h2>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  首先将Cell做好布局，调整到满意的位置和宽度，然后开始做Autolayout设定。
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  Autolayout操作方式有两种，一种是选择目标后，使用右下角的工具栏；另一种是直接使用右键拖拽目标，在弹出的菜单中选择限制项。当选择的目标比较小的时候，可以打开左侧的菜单，在这里做拖拽操作一样是可以的。个人感觉后者更方便一些。
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  开始之前，先来介绍下使用的基本工具吧。
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <span id="more-381" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit;"></span>
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  第一个按钮是和对齐有关的，就是控制多个元素（Lable, Button等）的统一约束。例如我们需要让标题和内容按照左，就选择标题和内容元素，选择Leading Edges设置为5即可。
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <a target="_blank" href="http://itony.me/wp-content/uploads/2013/12/Autolayout_Align.png" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer"><img src="http://itony.me/wp-content/uploads/2013/12/Autolayout_Align.png" alt="Autolayout_Align" width="357" height="352" class="alignnone size-full wp-image-393" style="border: 0px; max-width: 100%; height: auto;" /></a>
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  第二个按钮是和元素位置固定有关的限制条件，直接看图吧：
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <a target="_blank" href="http://itony.me/wp-content/uploads/2013/12/Autolayout_Pin.png" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer"><img src="http://itony.me/wp-content/uploads/2013/12/Autolayout_Pin.png" alt="Autolayout_Pin" width="295" height="382" class="alignnone size-full wp-image-397" style="border: 0px; max-width: 100%; height: auto;" /></a>
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  右侧能够看到当前选择元素限制条件的列表：
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <a target="_blank" href="http://itony.me/wp-content/uploads/2013/12/Autolayout_Inspector_Constrainsts-list.png" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer"><img src="http://itony.me/wp-content/uploads/2013/12/Autolayout_Inspector_Constrainsts-list.png" alt="Autolayout_Inspector_Constrainsts list" width="257" height="501" class="alignnone size-full wp-image-401" style="border: 0px; max-width: 100%; height: auto;" /></a><br />这里有两个参数，“Content Hugging Priority”和“Content Compression Resistance Priority”，感觉不太好理解，栈爆上找到一篇解释，讲的挺好的：<a target="_blank" href="http://stackoverflow.com/questions/15850417/cocoa-autolayout-content-hugging-vs-content-compression-resistance-priority" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer">Cocoa Autolayout: content hugging vs content compression resistance priority</a>
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#038;
#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  有时候想要一个元素的间距是一个动态值，例如距离右侧至少10pt（即>=10pt），那么可以在上图中点击右侧按钮(齿轮)进入详细设置：
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <a target="_blank" href="http://itony.me/wp-content/uploads/2013/12/Autolayout_Constraint_Relation-Config.png" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer"><img src="http://itony.me/wp-content/uploads/2013/12/Autolayout_Constraint_Relation-Config.png" alt="Autolayout_Constraint_Relation Config" width="260" height="184" class="alignnone size-full wp-image-394" style="border: 0px; max-width: 100%; height: auto;" /></a>
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  第三个按钮是有关清除限制条件、根据限制更新视图大小的工具。个人比较常用的是清除限制条件，有时候设置错了很麻烦，直接清除掉重新来就行了。
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <a target="_blank" href="http://itony.me/wp-content/uploads/2013/12/Autolayout_Resolve-Auto-Layout-Issues.png" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer"><img src="http://itony.me/wp-content/uploads/2013/12/Autolayout_Resolve-Auto-Layout-Issues.png" alt="Autolayout_Resolve Auto Layout Issues" width="470" height="245" class="alignnone size-full wp-image-395" style="border: 0px; max-width: 100%; height: auto;" /></a>
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  上面这些就是常用到的一些限制条件了。个人觉得使用右键拖拽弹出的菜单选择更方便和直观一些，因为菜单中会根据拖拽内容动态显示可用项供我们选择，菜单如图
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <a target="_blank" href="http://itony.me/wp-content/uploads/2013/12/Autolayout_ShortAction.png" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer"><img src="http://itony.me/wp-content/uploads/2013/12/Autolayout_ShortAction.png" alt="Autolayout_ShortAction" width="289" height="449" class="alignnone size-full wp-image-399" style="border: 0px; max-width: 100%; height: auto;" /></a>
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  大致就是这些了吧……
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  我来谈谈自己的用法。总体上是从上到下，从左到右做约束限制。在这个例子中，就是设置标题->内容->发帖人这样的顺序。
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  <a target="_blank" href="http://itony.me/wp-content/uploads/2013/12/Autolayout_Example.png" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer"><img src="http://itony.me/wp-content/uploads/2013/12/Autolayout_Example.png" alt="Autolayout_Example" width="373" height="138" class="alignnone size-full wp-image-398" style="border: 0px; max-width: 100%; height: auto;" /></a>
</p>

<ol style="margin-bottom: 1.5em; margin-left: 3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; list-style-position: initial; list-style-image: initial; color: rgb(102, 102, 102); line-height: 25px; white-space: normal;" class=" list-paddingleft-2">
  <li>
    <p>
      设置标题的顶部和左侧距离，以及宽度（防止超出边界）。
    </p>
  </li>
  
  <li>
    <p>
      设置内容的顶部（距离标题）和左侧距离，以及宽度。设置最大行数。
    </p>
  </li>
  
  <li>
    <p>
      设置发帖人的顶部和左侧距离，以及高度。
    </p>
  </li>
  
  <li>
    <p>
      设置发帖时间的顶部和左侧距离，距离右侧间距（防止内容过长）。
    </p>
  </li>
  
  <li>
    <p>
      <strong style="color: red;">关键步骤，设置发帖人距离底部距离，如果不设置这个参数，那么下面代码计算的Cell高度会永远是0。</strong>
    </p>
  </li>
</ol>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  多试一试，如果有错误或者缺少限制，XCode会有提示。它报出的错误一般都是必须修正的，但它给的自动修正建议有时并不是我们想要的（正确的），想清楚再添加。
</p>

<h2 style="margin: 40px 0px 15px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-weight: lighter; font-size: 1.6em; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Gr
ande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; clear: both; color: rgb(51, 51, 50); letter-spacing: -1px; line-height: 1; -webkit-hyphens: none; word-wrap: break-word; white-space: normal;">
  代码部分
</h2>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  使用了xib制作的Cell，那么在原来的项目代码中如何使用呢？看代码：
</p>

<textarea wrap="soft" class="crayon-plain print-no" data-settings="dblclick" readonly="" style="color: rgb(0, 0, 0); margin: 0px; vertical-align: top; border-width: 0px; border-top-left-radius: 0px; border-top-right-radius: 0px; border-bottom-right-radius: 0px; border-bottom-left-radius: 0px; overflow: hidden; padding: 0px 5px; width: 698px; height: 748px; position: absolute; opacity: 0; box-sizing: border-box; box-shadow: none; -webkit-box-shadow: none; white-space: pre; word-wrap: normal; resize: none; tab-size: 4; z-index: 0; line-height: 20px !important;"></textarea>

<table class="crayon-table" width="NaN">
  <tr class="crayon-row firstRow" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;">
    <td class="crayon-nums" data-settings="show" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-color: rgb(238, 238, 238) !important; background-position: 0px 50%;">
      <p>
        1
      </p>
      
      <p>
        2
      </p>
      
      <p>
        3
      </p>
      
      <p>
        4
      </p>
      
      <p>
        5
      </p>
      
      <p>
        6
      </p>
      
      <p>
        7
      </p>
      
      <p>
        8
      </p>
      
      <p>
        9
      </p>
      
      <p>
        10
      </p>
      
      <p>
        11
      </p>
      
      <p>
        12
      </p>
      
      <p>
        13
      </p>
      
      <p>
        14
      </p>
      
      <p>
        15
      </p>
      
      <p>
        16
      </p>
      
      <p>
        17
      </p>
      
      <p>
        18
      </p>
      
      <p>
        19
      </p>
      
      <p>
        20
      </p>
      
      <p>
        21
      </p>
      
      <p>
        22
      </p>
      
      <p>
        23
      </p>
      
      <p>
        24
      </p>
      
      <p>
        25
      </p>
      
      <p>
        26
      </p>
      
      <p>
        27
      </p>
      
      <p>
        28
      </p>
      
      <p>
        29
      </p>
      
      <p>
        30
      </p>
      
      <p>
        31
      </p>
      
      <p>
        32
      </p>
      
      <p>
        33
      </p>
      
      <p>
        34
      </p>
      
      <p>
        35
      </p>
      
      <p>
        36
      </p>
      
      <p>
        37
      </p>
    </td>
    
    <td class="crayon-code" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;" width="1010">
      <p>
        <span class="crayon-m" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">static</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSString</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">*CellIdentifier</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"CellIdentifier"</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        <span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&#8211;</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">void</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">viewDidLoad</span>
      </p>
      
      <p>
        <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//注册TableView中用于复用的Cell</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span
class="crayon-r" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">self</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> registerNib</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UINib</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> nibWithNibName</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"BBSPostContentCell"</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> bundle</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:nil</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> forCellReuseIdentifier</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:CellIdentifier</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//&#8230;</span>
      </p>
      
      <p>
        <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        <span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//关键方法，获取复用的Cell后模拟赋值，然后取得Cell高度</span>
      </p>
      
      <p>
        <span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&#8211;</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">CGFloat</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;">tableView</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UITableView</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important;
 line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">*</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> heightForRowAtIndexPath</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSIndexPath</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">*</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">indexPath</span>
      </p>
      
      <p>
        <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">BBSPostContentCell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">*cell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> dequeueReusableCellWithIdentifier</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:CellIdentifier</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSDictionary</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">*dataSourceItem</span><span class="crayon-h" style="m
argin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-r" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">self</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">dataSource</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> objectAtIndex</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:indexPath</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">row</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">titleLabel</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">text</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">dataSourceItem</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> valueForKey</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"title"</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: in
herit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">contentLabel</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">text</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">dataSourceItem</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> valueForKey</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"body"</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp; </span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-e" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;">cell </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">setNeedsUpdateConstraints</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-e" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;">cell </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">updateConstraintsIfNeeded</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">CGFloat</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: base
line; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">height</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">contentView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> systemLayoutSizeFittingSize</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:UILayoutFittingCompressedSize</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">height</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">return</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">height</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        <span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//在cellForRowAtIndexPath中，按照常规方法做赋值就行了</span>
      </p>
      
      <p>
        <span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&#8211;</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UITableViewCell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">*</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;">tableView</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="cra
yon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UITableView</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">*</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> cellForRowAtIndexPath</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSIndexPath</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">*</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">indexPath</span>
      </p>
      
      <p>
        <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">BBSPostContentCell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">*cell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> dequeueReusableCellWithIdentifier</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:CellIdentifier</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold
 !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSDictionary</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">*dic</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">dataSource</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">indexPath</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">row</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">titleLabel</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">text</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">dic</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"title"</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">contentLabel</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51,
51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">text</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">dic</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"body"</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </p>
      
      <p>
        <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">return</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
      </p>
      
      <p>
        <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
      </p>
    </td>
  </tr>
</table>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  2014.1.2: 在测试时发现这部分的代码还存在一些性能问题（整个表视图在更新时会卡顿），我会稍后补上。
</p>

<p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
  我在使用Instruments分析发现，heightForRowAtIndexPath中调用dequeueReusableCellWithIdentifier会占用很多CPU资源，因此我试着不使用registerNib方法注册复用Cell，而在代码中手动处理，类似这样：
</p>

<textarea wrap="soft" class="crayon-plain print-no" data-settings="dblclick" readonly="" style="color: rgb(0, 0, 0); margin: 0px; vertical-align: top; border-width: 0px; border-top-left-radius: 0px; border-top-right-radius: 0px; border-bottom-right-radius: 0px; border-bottom-left-radius: 0px; overflow: hidden; padding: 0px 5px; width: 698px; height: 148px; position: absolute; opacity: 0; box-sizing: border-box; box-shadow: none; -webkit-box-shadow: none; white-space: pre; word-wrap: normal; resize: none; tab-size: 4; z-index: 0; line-height: 20px !important;"></textarea>

<table class="crayon-table" width="NaN">
  <tr class="crayon-row firstRow" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;">
    <td class="crayon-nums" data-settings="show" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-color: rgb(238, 238, 238) !important; background-position: 0px 50%;">
      <p>
        1
      </p>
      
      <p>
        2
      </p>
      
      <p>
        3
      </p>
      
      <p>
        4
      </p>
      
      <p>
        5
      </p>
      
      <p>
        6
      </p>
      
      <p>
        7
      </p>
    </td>
    
    <td class="crayon-code" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;" width="775">
      <p>
        <span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">BBSPostContentCell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">*cell</ span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> dequeueReusableCellWithIdentifier</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:CellIdentifier</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span></p> 
        
        <p>
          <span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">if</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">==</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">nil</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
        </p>
        
        <p>
          <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">cell</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSBundle</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">mainBundle</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-e " style="margin: 0px; padding: 0px; outl
ine: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> loadNibNamed</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"BBSPostContentCell"</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> owner</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:self</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> options</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:NULL</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-cn" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 153, 153) !important;"></span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
        </p>
        
        <p>
          <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSLog</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"cell loadNibNamed"</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
        </p>
        
        <p>
          <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">else</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
        </p>
        
        <p>
          <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSLog</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"cell dequeueReusableCellWithIdentifier"</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
        </p>
        
        <p>
          <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
        </p></td> </tr> </tbody> </table> 
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#038;
#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          这时我发现这里的Cell调用dequeueReusableCellWithIdentifier方法总是返回nil，因此每次都是从xib中加载，从而耗费了大量的资源。问题的原因我还不清楚，目前我的解决方法是，单独生成一个Cell用于在heightForRowAtIndexPath方法中计算高度。
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          其次，在[tableView reloadData]和[tableView insertRowsAtIndexPaths]时，底层会将所有行高重新计算，这个会占用大量的时间，因此我试着对行高做了缓存，暂时解决了这个问题。
        </p>
        
        <h2 style="margin: 40px 0px 15px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-weight: lighter; font-size: 1.6em; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; clear: both; color: rgb(51, 51, 50); letter-spacing: -1px; line-height: 1; -webkit-hyphens: none; word-wrap: break-word; white-space: normal;">
          关于兼容性问题
        </h2>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          由于Autolayout只能在iOS6.0以上版本使用，而根据友盟统计，目前6.0以下的用户大概还有8%左右（2013.12）。现在有两个办法解决：
        </p>
        
        <ol style="margin-bottom: 1.5em; margin-left: 3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; list-style-position: initial; list-style-image: initial; color: rgb(102, 102, 102); line-height: 25px; white-space: normal;" class=" list-paddingleft-2">
          <li>
            <p>
              哥不在乎，放弃这些用户！（好霸气=。=）把项目的部署版本修改为6.0以上即可。
            </p>
          </li>
          
          <li>
            <p>
              咳…咳…这个嘛，用户还是有必要支持的………恩，那我们来说说这个怎么兼容。
            </p>
          </li>
        </ol>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          思路很简单，我们告诉XCode，6.0以上版本使用Autolayout，以下的旧版本不要使用这个就可以了。
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          将原xib文件inspector中选择”Interface Builder Document”->”Build for”->”iOS 6.0 and Later”，告诉XCode，这个xib在6.0以上设备编译。
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          将xib文件拷贝一份副本，命名为”xxx_iOS5.xib”，在inspector中选择”Project Deployment Target”，也就是说使用项目部署目标版本（即最低版本5.0），并取消”Use Autolayout”选项。
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          在代码中根据系统版本加载不同的xib文件：
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
        </p>
        
        <p>
          <textarea wrap="soft" class="crayon-plain print-no" data-settings="dblclick" readonly="" style="color: rgb(0, 0, 0); margin: 0px; vertical-align: top; border-width: 0px; border-top-left-radius: 0px; border-top-right-radius: 0px; border-bottom-right-radius: 0px; border-bottom-left-radius: 0px; overflow: hidden; padding: 0px 5px; width: 698px; height: 288px; position: absolute; opacity: 0; box-sizing: border-box; box-shadow: none; -webkit-box-shadow: none; white-space: pre; word-wrap: normal; resize: none; tab-size: 4; z-index: 0; line-height: 20px !important;"></textarea>
        </p>
        
        <table class="crayon-table" width="NaN">
          <tr class="crayon-row firstRow" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;">
            <td class="crayon-nums" data-settings="show" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-color: rgb(238, 238, 238) !important; background-position: 0px 50%;">
              <p>
                1
              </p>
              
              <p>
                2
              </p>
              
              <p>
                3
              </p>
              
              <p>
                4
              </p>
              
              <p>
                5
              </p>
              
              <p>
                6
              </p>
              
              <p>
                7
              </p>
              
              <p>
                8
              </p>
              
              <p>
                9
              </p>
              
              <p>
                10
              </p>
              
              <p>
                11
              </p>
              
              <p>
                12
              </p>
              
              <p>
                13
              </p>
              
              <p>
                14
              </p>
            </td>
            
            <td class="crayon-code" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;" width="1080">
              <p>
                <span class="crayon-p" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(184, 92, 0) !important;">#define SYSTEM_VERSION_GREATER_THAN_OR_EQUAL_TO(v) </span>
              </p>
              
              <p>
                <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-st
yle: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UIDevice</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">currentDevice</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> systemVersion</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> compare</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:v</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> options</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:NSNumericSearch</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">!=</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSOrderedAscending</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span>
              </p>
              
              <p>
                &nbsp;
              </p>
              
              <p>
                <span class="crayon-p" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(184, 92, 0) !important;">#define IS_SUPPORT_AUTOLAYOUT&nbsp;&nbsp; SYSTEM_VERSION_GREATER_THAN_OR_EQUAL_TO(@"6.0")</span>
              </p>
              
              <p>
                &nbsp;
              </p>
              
              <p>
                <span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&#8211;</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">void</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">viewDidLoad</span>
              </p>
              
              <p>
                <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">if</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-o" style="margin: 0px; paddin
g: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">!</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">IS_SUPPORT_AUTOLAYOUT</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> &nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//for iOS 5.x</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> &nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-r" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">self</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> registerNib</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UINib</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> nibWithNibName</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"BBSPostContentCell_iOS5"</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> bundle</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:nil</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> forCellReuseIdentifier</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:CellIdentifier</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">else</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="marg
in: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> &nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-r" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">self</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">.</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> registerNib</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">[</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UINib</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> nibWithNibName</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-s" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(221, 17, 68) !important;">@"BBSPostContentCell"</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> bundle</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:nil</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> forCellReuseIdentifier</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">:CellIdentifier</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">]</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
              </p>
              
              <p>
                <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
              </p>
            </td>
          </tr>
        </table>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          最后别忘了在高度计算时，区分下代码：
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
        </p>
        
        <p>
          <textarea wrap="soft" class="crayon-plain print-no" data-settings="dblclick" readonly="" style="color: rgb(0, 0, 0); margin: 0px; vertical-align: top; border-width: 0px; border-top-left-radius: 0px; border-top-right-radius: 0px; border-bottom-right-radius: 0px; border-bottom-left-radius: 0px; overflow: hidden; padding: 0px 5px; width: 698px; height: 248px; position: absolute; opacity: 0; box-sizing: border-box; box-shadow: none; -webkit-box-shadow: none; white-space: pre; word-wrap: normal; resize: none; tab-size: 4; z-index: 0; line-height: 20px !important;"></textarea>
        </p>
        
        <table class="crayon-table" width="NaN">
          <tr class="crayon-row firstRow" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0p
x !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;">
            </p> 
            
            <td class="crayon-nums" data-settings="show" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-color: rgb(238, 238, 238) !important; background-position: 0px 50%;">
              <p>
                1
              </p>
              
              <p>
                2
              </p>
              
              <p>
                3
              </p>
              
              <p>
                4
              </p>
              
              <p>
                5
              </p>
              
              <p>
                6
              </p>
              
              <p>
                7
              </p>
              
              <p>
                8
              </p>
              
              <p>
                9
              </p>
              
              <p>
                10
              </p>
              
              <p>
                11
              </p>
              
              <p>
                12
              </p>
            </td>
            
            <td class="crayon-code" style="outline: 0px; font-style: inherit; margin: 0px !important; padding: 0px !important; border: none !important; vertical-align: top !important; background-position: 0px 50%;" width="775">
              <p>
                <span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&#8211;</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">CGFloat</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;">tableView</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">UITableView</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">*</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">tableView</span><span class="crayon-e " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: teal !important;"> heightForRowAtIndexPath</span><span class="crayon-o" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">:</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">NSIndexPath</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-t " style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">*</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">indexPath</span>
              </p>
              
              <p>
                <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">if</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">(</span><span class="crayon-t" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important; color: rgb(128, 0, 128) !important;">IS_SUPPORT_AUTOLAYOUT</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">)</span><span class="c
rayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//Autolayout部分代码，同上</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//&#8230;..</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">return</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-v" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 45, 122) !important;">height</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">else</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">{</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp; </span><span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//for iOS 5.x</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp; </span><span class="crayon-c" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; height: inherit; font-style: italic !important; font-size: inherit !important; line-height: inherit !important; color: rgb(153, 153, 153) !important;">//为了简单起见，就直接使用固定值了，当然如果你要自己为iOS5用户手动计算动态高度，也是可以的。</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-st" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-weight: bold !important; font-size: inherit !important; line-height: inherit !important;">return</span><span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;"> </span><span class="crayon-cn" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 153, 153) !important;">81</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">;</span>
              </p>
              
              <p>
                <span class="crayon-h" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(0, 111, 224) !important;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
              </p>
              
              <p>
                <span class="crayon-sy" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; height: inherit; font-size: inherit !important; line-height: inherit !important; color: rgb(51, 51, 51) !important;">}</span>
              </p>
            </td>
          </tr>
        </table>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-fam
ily: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
        </p>
        
        <p style="margin-top: 0px; margin-bottom: 1.3em; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 17px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; line-height: 1.7em; color: rgb(102, 102, 102); white-space: normal;">
          完成了！
        </p>
        
        <p>
          <span style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-size: 13px; font-family: ff-tisa-web-pro-1, ff-tisa-web-pro-2, &#39;Lucida Grande&#39;, &#39;Hiragino Sans GB&#39;, &#39;Hiragino Sans GB W3&#39;, &#39;Microsoft YaHei&#39;, &#39;WenQuanYi Micro Hei&#39;, sans-serif; color: inherit; line-height: 19px; background-color: rgb(247, 247, 247);">原创文章，采用&nbsp;<a target="_blank" href="http://creativecommons.org/licenses/by-nc-sa/4.0/" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>&nbsp;进行许可。<br />转载请注明：转载自&nbsp;<a target="_blank" href="http://itony.me/" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer">Tony's blog</a>，原文网址：<a target="_blank" href="http://itony.me/381.html" style="margin: 0px; padding: 0px; outline: 0px; border: 0px; vertical-align: baseline; font-style: inherit; font-family: inherit; color: rgb(87, 173, 104); text-decoration: none;" rel="noopener noreferrer">http://itony.me/381.html</a></span>
        </p>