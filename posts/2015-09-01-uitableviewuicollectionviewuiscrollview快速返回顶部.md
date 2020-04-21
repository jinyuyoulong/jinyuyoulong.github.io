---
title: UITableView,UICollectionView,UIScrollView快速返回顶部
author: fan
type: post
date: 2015-09-01T10:53:57+00:00
url: /uitableviewuicollectionviewuiscrollview快速返回顶部/
duoshuo_thread_id:
  - 6278603326099555074
  - 6278603326099555074
views:
  - 12
  - 12
categories:
  - iOS
tags:
  - UICollectionView
  - UIScrollView
  - UITableView
  - 返回顶部

---
<span style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px; background-color: rgb(255, 255, 255);">UITableView， UICollectionView都继承自UIScrollView，所以可以使用UIScrollView的方法，设置显示内容的偏移量&nbsp;</span><br style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px; white-space: normal; background-color: rgb(255, 255, 255);" /><br style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px; white-space: normal; background-color: rgb(255, 255, 255);" /><span style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px; background-color: rgb(255, 255, 255);">[self.tableView setContentOffset:CGPointMake(0, 0) animated:YES];</span>