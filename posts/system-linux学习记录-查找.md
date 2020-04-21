---
title: Linux学习记录-查找
author: fan
type: post
date: 2019-04-01T13:58:16+00:00
excerpt: whereis 和 locate 利用文件数据库查找，速度比较快。推荐常用。find 功能强大。
url: /linux学习记录-查找/
categories:
  - 操作系统

---
whereis 和 locate 利用文件数据库查找，速度比较快。推荐常用。find 功能强大。

### whereis

寻找特定文件`whereis ifconfig`

### locate

可以文件名部分查找，`locate passwd`,查找迅速，文件数据库更新不及时，centOS 5.x 每天更新数据库一次。
  
依据 /var/lib/mlocate 内的数据库记载，找出用户输入的 key 文件名。

### find

直接查找硬盘。`find /etc -mtime 0` 按时间查找。`find / -name passwd` 查找文件名。