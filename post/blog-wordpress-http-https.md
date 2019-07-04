---
title: "Blog Wordpress Http Https"
date: 2019-05-07T17:58:56+08:00
draft: true
---

# wordpress http 升级HTTPS

1. lnmp 添加ssl：lnmp ssl add
2. wordpress 后台修改：主域名改为https:// ,固定链接改为id格式 (postname的URL格式无法找到，未解决)
3. 修改数据库,搜索数据库中的http的链接，修改为https
  `update wp_posts set post_content = replace(post_content, ‘http://www.v5u.win/’,‘https://www.v5u.win/’)`
4. 访问网站查找跨域引用(js,css)，更改代码或者数据库文本。改为https
