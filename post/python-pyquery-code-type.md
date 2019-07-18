---
title: pyquery 解析网页乱码
tags:
  - Python
  - 爬虫
id: 511
categories:
  - Python
date: 2016-11-18 10:08:22
---

### pyquery 解析网页乱码

`问题：使用pyquery直接请求的网页，解析中文出现一半乱码，一般正常的情况`

##### 花了半天的时间也没找到解决办法，第二天早上无意间点开一个搜索结果链接，经验证，完美解决问题，立字为证。

    1\. 确认encode设置正确
    2\. 根据知乎@actberw 的解释：pyquery的源码，http 请求使用的是requests，如果没有就调用标准库urllib2
    3\. requests可以很好的处理返回的html编码问题，而urllib2不能
    4\. 如果安装了requests还是不行的话，requests是有一个bug（2016年3月数据），有两种解决办法：
    1). 构建pq对象的时候把encoding参数传进去 d=pq(url='xxx', encoding="gbk")
    2). 把pyquery/openers.py 的_requests 函数中的 if encoding: resp.encoding = encoding 这两行换成 resp.encoding = encoding or None, 或者把 requests中get_encoding_from_headers 函数的后两行删除掉。
    3)（我的情况正好就是没有requests库，然后选择了方法一解决了问题）
    