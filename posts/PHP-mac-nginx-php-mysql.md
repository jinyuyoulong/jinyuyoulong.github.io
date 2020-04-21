---
title: mac-nginx-php-mysql
date: 2018-12-25 10:04:25
tags: [lnmp,nginx]
categories: [PHP]
---
[TOC]
### 安装环境

  * brew install nginx
  * brew install php
  * brew install mysql

### 配置环境

  * /usr/local/homebrew/etc/nginx/nginx.conf
  * /etc/php-fpm.conf

### 启动环境

  * brew services start nginx
  * php-fpm（启动php-fpm）

<hr class="wp-block-separator" />

#### nginx.conf

<pre class="wp-block-code"><code>server {
        location / {
            root   /rootDocument/;
            index  index.html index.htm index.php;
			autoindex on;                        #    //开启目录浏览功能；
            autoindex_exact_size off;            #//关闭详细文件大小统计，让文件大小显示MB，GB单位，默认为b
            autoindex_localtime on;              #//开启以服务器本地时区显示文件修改日期！
        }
        location ~ \.php$ {
            root           html;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME /rootDocument$fastcgi_script_name;
            include        fastcgi_params;
        }</code></pre>

#### php-fpm.conf

<pre class="wp-block-code"><code>error_log = /usr/local/homebrew/var/log/php-fpm.log #修改日志目录，防止权限问题</code></pre>