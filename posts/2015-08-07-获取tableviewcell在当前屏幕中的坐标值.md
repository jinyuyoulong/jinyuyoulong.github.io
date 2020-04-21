---
title: 获取tableviewCell在当前屏幕中的坐标值
author: fan
type: post
date: 2015-08-07T05:28:36+00:00
url: /获取tableviewcell在当前屏幕中的坐标值/
duoshuo_thread_id:
  - 6278603297523761921
  - 6278603297523761921
views:
  - 3
  - 3
categories:
  - iOS

---
获得当前cell对于当前屏幕的位置

<span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">CGRect&nbsp;rectInTableView&nbsp;=&nbsp;[tableView</span><span class="vars" style="margin: 0px; padding: 0px; border: none; color: rgb(221, 0, 0); background-color: inherit;">&nbsp;rectForRowAtIndexPath</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">:indexPath]; &nbsp;&nbsp;</span></span>

<span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;">CGRect&nbsp;rect&nbsp;=&nbsp;[tableView<span class="vars" style="margin: 0px; padding: 0px; border: none; color: rgb(221, 0, 0); background-color: inherit;">&nbsp;convertRect</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">:rectInTableView</span><span class="vars" style="margin: 0px; padding: 0px; border: none; color: rgb(221, 0, 0); background-color: inherit;">&nbsp;toView</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">:[tableView</span><span class="vars" style="margin: 0px; padding: 0px; border: none; color: rgb(221, 0, 0); background-color: inherit;">&nbsp;superview</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">]];</span></span>