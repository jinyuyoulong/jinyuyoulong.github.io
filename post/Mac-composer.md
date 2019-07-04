---
title: mac下安装composer
tags:
  - composer
  - PHP
id: 586
categories:
  - Mac
  - PHP
date: 2017-06-09 03:35:06
---

composer是PHP的包管理器

mac下如何安装呢？

最简单的方法是通过brew工具

brew install composer

这时候可能会遇到这个问题：

<span class="s1">Searching for a previously deleted formula...</span>

所以我们检查一下brew/core 中是否有composer可供安装

brew search composer

得到这个结果：

<span class="s1">homebrew/php/composer</span>

<span class="s1">homebrew/php/composer@1.2</span>

<span class="s1">caskroom/versions/multimarkdown-composer-beta</span>

<span class="s1">caskroom/cask/multimarkdown-composer-pro</span>

<span class="s1">caskroom/cask/multimarkdown-composer</span>

所以其实是有的，只是没找到

这时候我们通过brew 的 tap方法来设置一下

<span class="s1">brew tap homebrew/php</span>

完事之后，再运行brew install composer就可以了。

当然，还有其他的方法安装，但是我都不推荐，因为太麻烦！