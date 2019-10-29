---
title: go 常用命令
date: 2019-02-15 15:50:32
categories: [Go]
---

[TOC]

### go run

编译并运行Go源码文件，编译的可执行文件在tmp目录下，这会影响相对路径

### go build

编译源码文件，代码包，依赖包

### go get / go mod download xxx

动态获取远程代码包

go get 简介（1)
用于从远程代码仓库（如著名Github )上下载并安装代码包 

受支持的代码版本控制系统有：Git、Mercurial ( hg )、SVN、Bazaar 

指定的代码包会被下载到$G〇PATH中包含的第一个工作区的src目录中

```
常用命令参数
-d 只下载 不安装
-x 查看执行过程
-u 更新已下载的代码包
-fix 将旧版本的代码包转换成新版规则
```

```go
mac@name:~/go/golib/src/pkgtool$ go install -v -work
在源码目录下，执行 go install，会编译 a 文件到 
$HOME/golang/goc2p:
    bin/
    pkg/
        linux_386/
            pkgtool.a
        src/
```

例：go get github.com/hyper-carrot/go_lib/logging

### go install

go install简介( 1 )

​	用于编译并安装代码包或源码文件

​	安装代码包会在当前工作区的pkg/<平台相关目录>下生成归档文件

​	安装命令源码文件会在当前工作区的bin目录或$GOBIN目录下生成可执行文件

go install 简介(2 ) 		

​	执行该命令且不追加任何参数时，它会试图把当前目录作为代码包并安装 		

​	执行该命令且以代码包的导入路径作为参数时,该代码包及其依赖会被安装 		

​	执行该命令且以命令源码文件及相关库源码文件作为参数时，只有这些文件会被编译并安装

在源文件目录下，执行`go install` ,编译源码，可执行文件放在 $GOBIN 目录下。文件以当前目录的 name 为 name。例：

```go
cd webserver
go install
生成 bin/webserver
```

#### 交叉编译

CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go

没有使用 cgo 库，操作系统是Linux，CPU架构为amd64 