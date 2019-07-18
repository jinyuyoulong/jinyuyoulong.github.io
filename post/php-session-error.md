---
title: php session 不能跨页面传递
categories: 
- PHP
tags:
- PHP
---



session错误

1. 确认当前页面session有没有添加成功
2. debug可不可以讲session值跨页面传递
3. 设置php.ini文件session.auto_start=1,此时use_cookies=0，use_only_cookies=0

验证：

php -i 查看PHP配置

php.ini phpinfo()对比配置文件和实际环境配置

