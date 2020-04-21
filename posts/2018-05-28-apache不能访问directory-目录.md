---
title: Apache不能访问directory 目录
author: fan
type: post
date: 2018-05-28T06:14:25+00:00
excerpt: |
  <directory />
      AllowOverride none
      Allow from all
  </directory>
url: /apache不能访问directory-目录/
categories:
  - PHP
tags:
  - Apache
format: aside

---
Mac升级了系统，发现启动了Apache，可以访问index.php文件。
  
当目录下找不到文件的时候，应该显示Indexes目录，
  
此时报错`Forbidden 403 You don't have permission to access /www on this server`
  
原因是Apache2.2版config默认设置是：

    <Directory />
        AllowOverride none
        Allow from all
    </Directory>
    

Apache2.4 config默认设置是：

    <Directory />
        AllowOverride none
        Require all denied
    </Directory>
    

最佳方案，目标`<Directory>`下设置文件访问权限为:
  
`Allow from all`
  
参考：https://www.zyxware.com/articles/4550/solved-forbidden-you-dont-have-permission-to-access-on-this-server