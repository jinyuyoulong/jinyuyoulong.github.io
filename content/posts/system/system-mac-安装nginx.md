---
title: mac 安装nginx
author: fan
type: post
date: 2017-02-25T16:12:18+00:00
url: /mac-安装nginx/
categories:
  - Mac
tags:
  - nginx

---
安装
  
brew install nginx
  
启动
  
sudo nginx
  
重新启动
  
sudo nginx -s reload
  
停止
  
sudo nginx -s stop
  
ps 查看80端口占用情况
  
sudo lsof -P -itcp:80