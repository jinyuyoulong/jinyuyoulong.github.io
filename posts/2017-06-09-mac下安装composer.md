---
title: mac下安装composer
author: fan
type: post
date: 2017-06-09T03:35:06+00:00
url: /mac下安装composer/
categories:
  - Mac
  - PHP
tags:
  - PHP

---
composer是PHP的包管理器
  
mac下如何安装呢？
  
最简单的方法是通过brew工具
  
brew install composer
  
这时候可能会遇到这个问题：

<p class="p1">
  <span class="s1">Searching for a previously deleted formula&#8230;</span>
</p>

<p class="p1">
  所以我们检查一下brew/core 中是否有composer可供安装
</p>

<p class="p1">
  brew search composer
</p>

<p class="p1">
  得到这个结果：
</p>

<p class="p1">
  <span class="s1">homebrew/php/composer</span>
</p>

<p class="p1">
  <span class="s1">homebrew/php/composer@1.2</span>
</p>

<p class="p1">
  <span class="s1">caskroom/versions/multimarkdown-composer-beta</span>
</p>

<p class="p1">
  <span class="s1">caskroom/cask/multimarkdown-composer-pro</span>
</p>

<p class="p1">
  <span class="s1">caskroom/cask/multimarkdown-composer</span>
</p>

<p class="p1">
  所以其实是有的，只是没找到
</p>

<p class="p1">
  这时候我们通过brew 的 tap方法来设置一下
</p>

<p class="p1">
  <span class="s1">brew tap homebrew/php</span>
</p>

<p class="p1">
  完事之后，再运行brew install composer就可以了。
</p>

<p class="p1">
  当然，还有其他的方法安装，但是我都不推荐，因为太麻烦！
</p>