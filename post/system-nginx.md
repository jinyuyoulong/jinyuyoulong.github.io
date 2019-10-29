---
title: "Nginx 动态生成缩略图"
date: 2019-07-01T15:05:09+08:00
categories: [system]
tags: [nginx,PHP]
---

[TOC]

有的时候要生成大量尺寸的缩图，事先不知道有哪些尺寸，所以可以用php动态生成；

1.在nginx中配置

```nginx
location ~ ..(gif|jpg|jpeg|png|bmp)$
        {
                if ( !-f $request_filename) {
                        rewrite ^(.)/(.*)(\d+)(\d+).(gif|jpg|jpeg|png|bmp) /ImageTransferController.php?s=1/2_3_4.5;
                }
                expires      30d;
        }
```

2. 完善 ImageTransferController.php 文件

 