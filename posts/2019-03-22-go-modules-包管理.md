---
title: go modules 包管理
author: fan
type: post
date: 2019-03-22T08:35:56+00:00
url: /go-modules-包管理/
categories:
  - Go
tags:
  - Go
  - 包管理

---
### go modules

[TOC]

#### 环境配置

### 1.13 以后

```sh
go env -w GOPROXY=https://goproxy.cn,direct
```

1.13以前

    1. 正确配置 GOROOT</p> 
    2. `export GOPROXY="https://athens.azurefd.net" # 微软提供的公共代理，解决golang/x/tools 下载失败` 也可以以此技术建立自己的公共库

#### 初始化 同时 确定了项目的绝对目录路径

go mod init v5u.win/projectapi

生成 go.mod

导入包：`import "v5u.win/projectapi/src/app/service"`

#### 添加依赖

go mod tidy

#### 生成 go.sum 自动添加依赖关系到 go.mod

`go run main.go`

#### 下载依赖包

`go mod download github.com/pelletier/go-toml`

#### Tips:

  1. 不能在 golib/src 下创建项目
  2. 在 Go1.11 版本下，GOPATH 目录中的项目默认是禁用 Go Module 的，需要手动开启
  3. export GOPROXY=&#8221;https://athens.azurefd.net&#8221; // 微软提供的公共代理
  4. export export GO111MODULE=on // 必须使用module依赖，在src/ 目录下可以使用module

#### 常用命令

<pre><code class="language-shell line-numbers">go mod tidy //拉取缺少的模块，移除不用的模块。
go mod download //下载依赖包
go mod graph //打印模块依赖图
go mod vendor //将依赖复制到vendor下,目前貌似只会下载你代码中引用的库，而不是go.mod中定义全部的module。坑
go mod verify //校验依赖
go mod why //解释为什么需要依赖
go list -m -json all //依赖详情
</code></pre>