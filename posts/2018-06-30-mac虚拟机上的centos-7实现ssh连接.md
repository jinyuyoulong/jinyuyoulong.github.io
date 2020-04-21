---
title: mac虚拟机上的centos 7实现ssh连接
author: fan
type: post
date: 2018-06-30T08:57:11+00:00
url: /mac虚拟机上的centos-7实现ssh连接/
categories:
  - Mac
  - 其他技术
  - 工具
  - 操作系统
tags:
  - centos
  - Mac
format: aside

---
mac虚拟机上的centos7实现ssh连接

  1. 查看是否安装ssh rpm -qa | grep ssh（一般都内置了）

  2. 配置sshd\_config文件 /etc/ssh/sshd\_config

    Port 22
    ListenAddress 0.0.0.0
    ListenAddress ::
    

  1. 防火墙配置

    1. 安装iptables: yum install iptables-service
    2. 配置防火墙文件：vim /etc/sysconfig/iptables
    3. 关闭防火墙：systemctl restart iptables.service
    4. systemctl enable iptables.service //设置防火墙开机启动
    

  1. 安装netstat：yum install net-tools （查看监听端口：netstat -ntpl | grep 22）
  2. 关闭虚拟机，设置虚拟机网络为host-only方式，virtualbox需要设置全局设置

    1. cmd+,->网络->仅主机(host-only)网络
    2. 添加网络
    

  1. 查看虚拟机ip地址，ip `ip addr`
  2. 主机找到可以ping 通的ip
  3. ssh登录 ssh root@192.168.xx.xx