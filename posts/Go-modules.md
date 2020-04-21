---
title: Go modules
date: 2019-04-03
categories: [Go]
---



### go modules

[TOC]

## go 1.13 的环境配置

删除.zshrc 中的大部分配置，只配置goroot其余配置用下列命令：

```sh
go env -w GOSUMDB="sum.golang.google.cn" # 更换为国内的校验源，默认sum.golang.org
go env -w GOPROXY="https://goproxy.io,direct" # 解决代理
go env -w GO111MODULE="on"
go env -w GOPRIVATE=*.gitlab.com,*.gitee.com # 代理跳过私有库设置
```

---

#### 环境配置

1. 正确配置 GOROOT

2. `export GOPROXY="https://goproxy.cn,direct" # 七牛提供的公共代理，解决golang/x/tools 下载失败`

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
3. export GOPROXY="https://goproxy.cn,direct" // 微软提供的公共代理,也可以以此技术建立自己的公共库
4. export export GO111MODULE=on // 必须使用module依赖，在src/ 目录下可以使用module。 go1.13已经全面支持

一条 `go env-w GOPROXY=https://goproxy.cn,direct`即可。之所以在后面拼接一个 `,direct`，是因为通过这样做我们可以在一定程度上解决私有库的问题（当然， goproxy.cn 无法访问你的私有库）

#### 常用命令

```sh
go mod tidy //拉取缺少的模块，移除不用的模块。
go mod download //下载依赖包
go mod graph //打印模块依赖图
go mod vendor //将依赖复制到 vendor 下
go mod verify //校验依赖
go mod why //解释为什么需要依赖
go list -m -json all //依赖详情
```

### 注：

module vgo 默认使用本地缓存的代码版本，如果想指定版本的话，最好显示声明一下，不要使用自动解析的方式。

file go.mod

```go
module giligili

go 1.13

require (
	github.com/gin-gonic/gin v1.4.0
	github.com/go-redis/redis v6.15.5+incompatible
	github.com/jinzhu/gorm v1.9.10
)

```

### 引入本地依赖包

前面铺垫了这么多，接下来回到我们的主题，我该怎样使用我们自己开发的工具包呢？ 假设我们有一个新的项目 `testmod-demo`，现在想要在新的项目中使用 testmod 中的工具包，那么首先我们需要使用 `go mod` 初始化该项目：

```shell
cd testmod-demo
go mod init gitee.com/rockyang/testmod-demo
```

初始化之后会在当前项目根目录生成一个 `go.mod`，接下来我们有两种方式去引入 testmod 包，一种是直接修改 `go.mod` 文件，在 require 配置中添加上

```shell
gitee.com/rockyang/testmod v0.0.0-20190610103414-4c55783279db
```

或者使用 `go mod edit` 命令修改依赖

```shell
go mod edit -require="gitee.com/rockyang/testmod@v0.0.0-20190610103414-4c55783279db"
go mod tidy # 整理依赖包
```

### 使用 replace 将远程包替换为本地包服务

这时如果你执行 `go build` 的时候会报错，提示找不到 `gitee.com/rockyang/testmod`，是因为你没有把仓库推送到远程，所以无法下载。 go module 提供了另外一个方案, 使用 replace, 编辑 go.mod 文件，在最后面添加： `replace gitee.com/rockyang/testmod => /gopath/src/gitee.com/rockyang/testmod`

```shell
module gitee.com/rockyang/testmod-demo

go 1.12

require (
    github.com/gin-gonic/gin v1.3.0
	gitee.com/rockyang/testmod@v0.0.0-20190610103414-4c55783279db
    golang.org/x/net v0.0.0-20190320064053-1272bf9dcd53 // indirect
)

replace gitee.com/rockyang/testmod => /gopath/src/gitee.com/rockyang/testmod
```

> 这里的 /gopath/src/gitee.com/rockyang/testmod 是本地的包路径

然后再执行 `go build` 你会看到你想要的结果。

## 私有库相关设置

首先私有服务器必须有一个域名，不能使用ip。

这里使用 gitee 和 GitHub 作为测试服务器

```sh
GOSUMDB=off #解决私有库校验不过，放弃校验，大心脏者适用
GOSUMDB=sum.golang.google.cn #或者 更换校验源
go env -w GOSUMDB="sum.golang.google.cn" # google 为我们提供了国内的校验源
```

配置 .gitconfig 将 http 改为 ssh 获取。

```sh
[http]
	extraheader = PRIVATE-TOKEN: token
[url "git@gitee.com:fan.jinlong/go_module_lib.git"]
	insteadOf = https://gitee.com/fan.jinlong/go_module_lib.git
```



坑4:拉取私有模块

![image](https://image.eddycjy.com/075bdc3d3552c000981c9d4fdd8d0f3f.jpg)

这里主要想涉及两块知识点，如下：

\- GOPROXY 是无权访问到任何人的私有模块的，所以你放心，安全性没问题。
\- GOPROXY 除了设置模块代理的地址以外，还需要增加 “direct” 特殊标识才可以成功拉取私有库。