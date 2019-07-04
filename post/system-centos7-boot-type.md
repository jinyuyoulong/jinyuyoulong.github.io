---
title: centos7 更改系统启动模式
tags:
  - centos
url: 753.html
id: 753
categories:
  - 操作系统
date: 2018-06-26 01:51:41
---

centos7 更改系统启动模式

1.  查看当前启动模式 systemctl get-default
2.  查看配置文件 cat /etc/inittab
3.  设置启动模式为命令行模式 systemctl set-target multi-user.target
4.  重启 shutdown -r now