---
title: WordPress中各个全局函数的含义和应用
author: fan
type: post
date: 2015-08-18T02:10:38+00:00
url: /wordpress中各个全局函数的含义和应用/
duoshuo_thread_id:
  - 6278603325105505026
  - 6278603325105505026
views:
  - 2
  - 2
categories:
  - PHP

---
<p class="p1">
  <span class="s1">在wordpress插件和主题开发中经常需要获取各种URL路径，wordpress提供了以下集中方法获得URL路径：</span>
</p>

<p class="p1">
  <span class="s1">plugins_url() — 插件目录的 URL (例如：http://www.hujuntao.com/wp-content/plugins)</span>
</p>

<p class="p1">
  <span class="s1">includes_url() — includes 目录的 URL (例如：http://www.hujuntao.com/wp-includes)</span>
</p>

<p class="p1">
  <span class="s1">content_url() — content 目录的 URL (例如：http://www.hujuntao.com/wp-content)</span>
</p>

<p class="p1">
  <span class="s1">admin_url() — admin 目录的 URL (例如：http://www.hujuntao.com/wp-admin/)</span>
</p>

<p class="p1">
  <span class="s1">site_url() — 当前网站的 URL (例如：http://www.hujuntao.com)</span>
</p>

<p class="p2">
  <span class="s2">home_url() — 当前网站首页的 URL (例如：<a href="http://www.hujuntao.com)" _src="http://www.hujuntao.com)">http://www.hujuntao.com)</a> </span>
</p>

<p class="p2">
  总结就是：
</p>

<p class="p1">
  <span class="s1">获得首页地址 ==> home_url()、bloginfo(‘url’)、get_bloginfo(‘url’)、get_home_url()。home_url() 3.0加入的函数，为了兼容老版本推荐使用bloginfo();</span>
</p>

<p class="p1">
  <span class="s1">获得安装路径 ==> site_url()、bloginfo(‘wpurl’)、get_bloginfo(‘wpurl’)、get_site_url()。</span>
</p>

<p class="p2">
  <span class="s2">如果你需要返回值 ==> get_bloginfo(‘url’)、get_home_url()/get_bloginfo(‘wpurl’)、get_site_url() 如果你想直接输出值 ==></span>
</p>