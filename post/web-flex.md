---
title: flex属性
id: 385
categories:
  - web前端
date: 2016-04-08 10:56:38
tags:
---

<table>
<thead>
<tr>
  <th>流式布局</th>
</tr>
</thead>
<tbody>
<tr>
  <td>flex为可伸缩属性，当flex大于0时View可伸缩 当多个有flex属性的View时，根据flex值分配View的相对大小，</td>
</tr>
<tr>
  <td>如`&lt;superView style={flex:1}&gt;&lt;View1 style={flex:5}&gt;&lt;/View1&gt;&lt;View2 style={flex:10}&gt;&lt;/View2&gt;&lt;/superView&gt;`</td>
</tr>
<tr>
  <td>则5+10=15View1占superView的5/15大小，View2是superView的10/15</td>
</tr>
<tr>
  <td>flexDirection:设定布局方向 value值为: row(横向布局)，column(纵向布局)</td>
</tr>
<tr>
  <td>alignSelf:对齐方式 主要有四种：flex-start(left居左)、 flex-end(right居右)、 center、  auto(默认自动)、 stretch。</td>
</tr>
</tbody>
</table>