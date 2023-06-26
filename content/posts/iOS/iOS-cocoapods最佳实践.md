---
title: "Cocoapods最佳实践"
date: 2021-04-19T15:49:24+08:00
toc: true
tags: 
  - Cocoapods
---

对于cocoapods的最佳实践有这么几个问题需要回答：
1. cocoapods使用过程中有什么问题
2. 如何解决，基于什么原理

### cocoapods使用过程中有什么问题？
主要是遇到多人协作和多项目协作时，每个人的本地Ruby版本和cocoapod版本不一致，有可能会导致一些无法预料的问题，和沟通上的成本。比如：对同一个问题的描述，看到的问题不一样，原因是pod版本不同导致的。
### 如何解决，基于什么原理？
cocoapods实际上是一个Ruby的第三方包，基于Ruby的包管理，我们可以管理cocoapods，然后我们基于cocoapods管理iOS上的第三方包。
使用 gem gvm 进行版本管理

```shell
brew install rbenv
rbenv install 2.7.0 # 安装ruby版本
rbenv shell 2.7.0 # 使版本生效
gem pristine --all # 切换ruby版本后 执行，不然有些库bundle找不到
ruby --version # 检查版本
ruby 2.7.0p0 (2019-12-25 revision 647ee6f091) [x86_64-darwin19]
which ruby # 查看 ruby 位置
/Users/gua/.rbenv/shims/ruby
which gem # 查看 gem 位置
/Users/bytedance/.rbenv/shims/gem
```



```ruby
file：Gemfile
# frozen_string_literal: true

source "https://rubygems.org"

git_source(:github) {|repo_name| "https://github.com/#{repo_name}" }

# gem "rails"
gem "cocoapods", "1.9.3"
```
Bundler 能够跟踪并安装所需的特定版本的 gem，以此来为 Ruby 项目提供一致的运行环境。

Bundler 是 Ruby 依赖管理的一根救命稻草，它可以保证你所要依赖的 gem 如你所愿地出现 在开发、测试和生产环境中。 利用 Bundler 启动项目简单到只用一条命令：`bundle install`。

> Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed.

> Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production. Starting work on a project is as simple as `bundle install`.

开始一个项目的工作很简单bundle install。
bundle exec pod install
bundle exec gem list
执行 bundle install 拿到别人的项目，执行这个，下载好依赖的ruby库
新项目使用顺序：

0. 创建一个xcode项目
1. bundle init
首先先来初始化一个 Bundler 环境（其实就是自动创建一个 Gemfile 文件）：请参考上文Gemfile
2. bundle exec pod init 创建Podfile文件
3. bundle exec pod install 配置完pod依赖库后执行pod 初始化
4. over

本文参考：[知识小集](https://mp.weixin.qq.com/s/fo5MNM9WpknvvehYo4V1Qw) 以及自己使用过程中遇到的问题