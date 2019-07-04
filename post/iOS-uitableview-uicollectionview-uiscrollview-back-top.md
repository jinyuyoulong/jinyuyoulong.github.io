---
title: 'UITableView,UICollectionView,UIScrollView快速返回顶部'
tags:
  - UICollectionView
  - UIScrollView
  - UITableView
  - 返回顶部
id: 189
categories:
  - iOS
date: 2015-09-01 18:53:57
---

<span style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px; background-color: rgb(255, 255, 255);">UITableView， UICollectionView都继承自UIScrollView，所以可以使用UIScrollView的方法，设置显示内容的偏移量&nbsp;</span>

<span style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.2000007629395px; background-color: rgb(255, 255, 255);">[self.tableView setContentOffset:CGPointMake(0, 0) animated:YES];</span>