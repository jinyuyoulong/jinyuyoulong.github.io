---
title: "Go Nginx反向代理"
date: 2019-05-10T16:08:55+08:00
draft: true
categories:
  - Go
---

当我们启动一个go 程序的时候，通常监听的是本地端口如 IP:port 。但是实际的线上环境，解析路径是：通过 DNS 解析 ——> nginx vhost ——> IP:port 这个。单纯的使用 go 是不能处理 域名解析工作的。
所以通常是NGINX 和 Go 搭配着使用。

nginx 可以帮我做很多工作，例如访问日志，cc 攻击，静态服务等，nginx 已经做的很成熟了。
Go 只要专注于业务逻辑和功能就好。
NGINX作为反向代理的配置如下：
```nginx
#列出所有服务器地址，nginx 自动均衡分发请求到各个服务器。 
upstream frontends {   
    ip_hash; 
    server 192.168.199.1:8088;
    server 192.168.199.2:8089;
}
server
    {
        listen 80;
        server_name nav.v5u.win ;

	#静态资源交由nginx管理
   	 location /static {
        root        /var/www/mydomain/web;
        expires     1d;
        add_header  Cache-Control public;
        access_log  off;
    	}

		# 反向代理设置
		location ~ /
			{
				proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
				proxy_set_header Host $http_host;
				proxy_redirect off;
				proxy_pass http://localhost:7070;
			}
	}
```

