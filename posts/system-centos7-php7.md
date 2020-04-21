---
title: centos7 PHP7环境配置
tags: [centos,php,system]
categories: [system]
date: 2018-06-26 01:50:27
---

centos7 PHP7环境配置 目录 1. 开启22端口2. 创建其他用户，使用其他用户ssh登录（root账户禁止登录）3. 关闭防火墙4. 关闭selinux5. 安装Apache6. 安装MySQL7. 安装PHP7.28. 配置 \[TOC\]

1.  开启22端口
    
2.  创建其他用户，使用其他用户ssh登录（root账户禁止登录）
    

ssh test@10.211.55.5 (使用eth0网卡IP)

1.  关闭防火墙

    centos7 默认使用firewalld，不在内置iptables
    //临时关闭
    systemctl stop firewalld
    //禁止开机启动
    systemctl disable firewalld
    

1.  sudo yum -y install iptables-services
2.  sudo vi /etc/sysconfig/iptables
3.  systemctl restart iptables.service （重启）
4.  systemctl enable iptables.service （开机自启动iptables）注：并不能开机自动关闭firewalld
    
5.  关闭selinux
    

gedit /etc/sysconfig/selinux

1.  安装Apache
    
2.  sudo yum install httpd
    
3.  sudo service httpd start
4.  service httpd state
    
5.  安装MySQL
    

sudo yum install mysql-server （失败）

1.  安装PHP7.2
    
2.  sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
    
3.  yum install yum-utils
4.  yum-config-manager --enable remi-php72
5.  yum install php php-mcrypt php-cli php-gd php-curl php-mysql php-ldap php-zip php-fileinfo (安装PHP模块)
6.  php -v
    
7.  配置
    
8.  sudo chkconfig httpd on （Apache重启）
    
9.  sudo nano /var/www/html/info.php （编辑PHP文件）
10.  sudo service httpd restart
11.  sudo vi /var/www/html/index.php (添加并编辑index.php)
12.  修改Apache配置文件 /etc/httpd/conf/httpd.conf