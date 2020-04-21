---
title: xorm cmd 墙内安装
author: fan
type: post
date: 2019-03-11T07:12:34+00:00
excerpt: |
  有两个库不能墙内访问 civil crypto.所以我们需要迂回一下安装。
  可以直接用 git clone github.com 上的库。这两个库都可以在GitHub上找到。
url: /xorm-墙内安装/
categories:
  - Go
tags:
  - orm

---
##### xorm cmd 墙内安装

有两个库不能墙内访问 civil crypto.所以我们需要迂回一下安装。
  
可以直接用 git clone github.com 上的库。这两个库都可以在GitHub上找到。

<pre><code class="line-numbers">go get github.com/go-xorm/cmd/xorm
失败 timeout
cd ($GOPATH/src)/golang.org/x
git clone https://github.com/golang/crypto.git
cd ($GOPATH)/src/cloud.google.com/
git clone  https://github.com/googleapis/google-cloud-go.git
cd cloud.google.com 将 google-cloud-go 目录名更改为 go
go install github.com/go-xorm/cmd/xorm 安装成功
</code></pre>

##### 使用

先设计MySQL数据表，在执行命令，生成 models
  
生成代码直接使用

<pre><code class="language-sh line-numbers">xorm reverse mysql "username:pwd@tcp(127.0.0.1:3306)/dbname?charset=utf8" $GOPATH/src/github.com/go-xorm/cmd/xorm/templates/goxorm
</code></pre>

格式：xorm reverse dirver dbname 导出模板