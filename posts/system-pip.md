---
title: mac下 pip 设置豆瓣源
tags: [pip,Python]
categories: [Python]
date: 2017-10-19 07:18:14
---

在用户目录下创建文件夹.pip，在.pip下创建pip.conf
pip.conf填入内容
[global]
index-url = https://pypi.douban.com/simple
[list]
format=columns