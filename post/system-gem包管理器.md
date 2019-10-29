---
title: gem 包管理器
id: 247
categories:
  - iOS
date: 2015-11-12 15:33:43
tags:
---

gem 常用命令

查看软件源 `gem source -l`,不能翻墙的，建议改成国内的源 https://gems.ruby-china.com

移除某个源 `gem sources --remove https://ruby.taobao.org/`

添加新的源 `gem sources -a https://gems.ruby-china.com/ `


安装 gem install [name] `gem install cocoapods`

卸载指定版本 `sudo gem uninstall cocoapods --version=1.5.3`

查看 `gem list` cocoapods (1.7.4, 1.7.1, 1.5.3) 代表当前安装有三个版本，版本号是()里面的。

sudo 安装的包是安装在系统目录下 /Library/Ruby/Gems/2.3.0/gems

推荐不使用sudo命令,此时 gem的安装目录为 ~/.gem/

教程学习来这里 https://guides.rubygems.org/

