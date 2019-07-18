---
title: Wordpress中各个全局函数的含义和应用
id: 169
categories:
  - PHP
date: 2015-08-18 10:10:38
tags:
---

<span class="s1">在wordpress插件和主题开发中经常需要获取各种URL路径，wordpress提供了以下集中方法获得URL路径：</span>

<span class="s1">plugins_url() — 插件目录的 URL (例如：http://www.hujuntao.com/wp-content/plugins)</span>

<span class="s1">includes_url() — includes 目录的 URL (例如：http://www.hujuntao.com/wp-includes)</span>

<span class="s1">content_url() — content 目录的 URL (例如：http://www.hujuntao.com/wp-content)</span>

<span class="s1">admin_url() — admin 目录的 URL (例如：http://www.hujuntao.com/wp-admin/)</span>

<span class="s1">site_url() — 当前网站的 URL (例如：http://www.hujuntao.com)</span>

<span class="s2">home_url() — 当前网站首页的 URL (例如：[http://www.hujuntao.com)](http://www.hujuntao.com)) </span>

总结就是：

<span class="s1">获得首页地址 ==&gt; home_url()、bloginfo(‘url’)、get_bloginfo(‘url’)、get_home_url()。home_url() 3.0加入的函数，为了兼容老版本推荐使用bloginfo();</span>

<span class="s1">获得安装路径 ==&gt; site_url()、bloginfo(‘wpurl’)、get_bloginfo(‘wpurl’)、get_site_url()。</span>

<span class="s2">如果你需要返回值 ==&gt; get_bloginfo(‘url’)、get_home_url()/get_bloginfo(‘wpurl’)、get_site_url() 如果你想直接输出值 ==&gt;</span>