---
title: mac下 pip 设置豆瓣源
author: fan
type: post
date: 2017-10-19T07:18:14+00:00
url: /mac下-pip-设置豆瓣源/
categories:
  - Python
tags:
  - pip
  - Python

---
在用户目录下创建**文件夹**.pip，在.pip下创建pip.conf
  
pip.conf填入内容
  
[global]
  
index-url = https://pypi.douban.com/simple
  
[list]
  
format=columns