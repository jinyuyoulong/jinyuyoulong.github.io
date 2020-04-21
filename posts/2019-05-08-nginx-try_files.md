---
title: nginx try_files
author: fan
type: post
date: 2019-05-08T02:10:48+00:00
url: /nginx-try_files/
categories:
  - PHP
  - 操作系统

---
## 源起：

WordPress http 升级成 https 之后，只有 首页可以正常访问，其他链接均失效，改固定链接为 `?p=id`可以正常显示，但是以前的 Google 收录页面面临失效的风险。遂着手解决。

### 发现解决方案，修改 nginx.conf 配置

<pre><code class="language-nginx line-numbers">location / {
            #如果文件不存在则尝试重定向解析
            try_files  $uri $uri/ /index.php?q=$uri&$args
}
</code></pre>

### 探求原理

try_files指令说明

<pre><code class="language-nginx line-numbers">try_files指令
语法：try_files file ... uri 或 try_files file ... = code
默认值：无
作用域：server location
</code></pre>

nginx 在0.7以后的版本中加入了一个 try_files 指令，配合命名 location，可以部分替代原本常用的 rewrite 配置方式，提高解析效率。
  
其作用是按顺序检查文件是否存在，**返回第一个找到的文件或文件夹**(结尾加斜线表示为文件夹)，如果所有的文件或文件夹都找不到，会进行一个内部重定向到最后一个参数。
  
参考文章 https://www.hi-linux.com/posts/53878.html