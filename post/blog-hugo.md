---
title: "Hugo 开箱体验"
date: 2019-04-16T14:09:31+08:00
categories: [blog]
---



Hugo是Go写的静态网站生成器，生成速度快，性能开销小，正好也在学习Golang。我决定从 Hexo 切换到 Hugo。

以下是试用总结，基本可以实现从0到1。至于从1到n，同学们加油！

### 安装

`brew install hugo`

### 创建站点

`hugo new site path/blogname`

### 创建页面

`hugo new post/first.md ` 默认文章创建位置为content目录

### 预览

`hugo server --theme=maupassant --buildDrafts`

### 生成静态页

直接运行`hugo` 单命令就可以生成 public 目录，内放生成的静态页面

### 发布

使用 git或其他方式 将public目录下的文件发布到目标地址

### 其他

`hugo new theme themename` 创建 theme