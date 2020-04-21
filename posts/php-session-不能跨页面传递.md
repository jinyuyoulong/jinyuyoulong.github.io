---
title: php session 不能跨页面传递
author: fan
type: post
date: 2019-01-16T06:15:18+00:00
url: /php-session-不能跨页面传递/
categories:
  - PHP

---
* * *title: php session 不能跨页面传递


  
categories: PHP</p> 

## tags: PHP

session错误

  1. 确认当前页面session有没有添加成功
  2. debug可不可以讲session值跨页面传递
  3. 设置php.ini文件session.auto\_start=1,此时use\_cookies=0，use\_only\_cookies=0

验证：
  
php -i 查看PHP配置
  
php.ini phpinfo()对比配置文件和实际环境配置