---
title: MySQL8
author: fan
type: post
date: 2019-03-20T05:58:16+00:00
excerpt: Navicat 连接 mysql8 的解决方案有三：
url: /mysql8/
categories:
  - 其他技术
  - 操作系统
tags:
  - mysql

---
mysql5.7 —>mysql8 的升级
  
MySQL8的加密方式有变化
  
命令行查看MySQL8 账户的加密方式

<pre><code class="language-mysql line-numbers">use mysql;
select user,plugin from user ;
</code></pre>

在mysql8之前的版本使用的密码加密规则是`mysql_native_password`，但是在mysql8则是`caching_sha2_password`。
  
Navicat不支持 caching\_sha2\_password 这种加密方式，所以升级后 Navicat 不能连接 MySQL8

#### Navicat 连接 mysql8 的解决方案有三：

##### 方案一 重新创建一个账号，设此账号的加密方式为 mysql\_native\_password，使用这个账号

create user &#8216;fanjinlong&#8217;@&#8217;%&#8217; identified with mysql\_native\_password by &#8216;333&#8217;;
  
create user &#8216;your username&#8217;@&#8217;%&#8217; identified with caching\_sha2\_password by &#8216;your password&#8217;;
  
ps. 此路不通，该账号无法创建 database 和 table

##### 方案二 修改root 的密码加密方式，刷新

ALTER USER &#8216;root&#8217;@&#8217;localhost&#8217; IDENTIFIED BY &#8216;password&#8217; PASSWORD EXPIRE NEVER; # 更改root 的加密方式
  
ALTER USER &#8216;root&#8217;@&#8217;localhost&#8217; IDENTIFIED WITH mysql\_native\_password BY &#8216;password&#8217;;# 重置密码
  
FLUSH PRIVILEGES; #刷新数据库

##### 方案三 更换MySQL8 客户端

关于 caching\_sha2\_password
  
MySQL提供了两个身份验证插件，可以为用户帐户密码实现SHA-256哈希：
  
sha256_password：实现基本的SHA-256身份验证。
  
caching\_sha2\_password：实现SHA-256身份验证（如sha256_password），但在服务器端使用缓存以获得更好的性能，并具有更广泛的适用性的附加功能。

> 在MySQL 8.0中，caching\_sha2\_password是默认的身份验证插件而不是 mysql\_native\_password。
    
> 要使用通过caching\_sha2\_password插件进行身份验证的帐户连接到服务器，您必须使用安全连接或支持使用RSA密钥对进行密码交换的未加密连接，如本节后面所述。无论哪种方式， caching\_sha2\_password插件都使用MySQL的加密功能。