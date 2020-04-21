---
title: mac中如何卸载pkg包
author: fan
type: post
date: 2019-03-19T07:00:08+00:00
url: /mac中如何卸载pkg包/
categories:
  - Mac
  - 工具
  - 操作系统

---
# mac中如何卸载pkg包

&#8220;\`
  
pkgutil &#8211;pkgs
  
cd /private/var/db/receipts
  
ls
  
lsbom com.apple.pkg.JavaForMacOSX107.bom //查看所有关联文件。