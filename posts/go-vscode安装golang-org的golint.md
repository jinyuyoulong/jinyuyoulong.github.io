---
title: vscode安装golang.org的golint
date: 2019-02-15
categories: [Go]
---
vscode 安装了 go 插件后，一些 Extensions 无法通过 vscode 自动安装，此时可以手动从控制台安装。下面是一些基础标准库

<pre><code class="language-go line-numbers">go get -u -v github.com/nsf/gocode
go get -u -v github.com/rogpeppe/godef
go get -u -v github.com/zmb3/gogetdoc
go get -u -v github.com/golang/lint/golint
go get -u -v github.com/lukehoban/go-outline
go get -u -v sourcegraph.com/sqs/goreturns
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v github.com/tpng/gopkgs
go get -u -v github.com/newhook/go-symbols
go get -u -v golang.org/x/tools/cmd/guru
go get -u -v github.com/cweill/gotests/...
</code></pre>

其中 golint guru gorename 需要手动编译。

因为GitHub中的golint需要拉取golang.org中的资源，但是golang.org资源无法获取。所以需要手动编译安装。

##### 安装golint：

  1. `cd $GOPATH/src` 进入 GOPATH 目录下</p> 
  2. `mkdir golang.org/x` 创建 golang.org/x 目录

  3. `cd golang.org/x`

  4. `git clone https://github.com/golang/tools.git tools` 下载 golang tools

  5. `git clone https://github.com/golang/lint` git clone golang/lint (如果github.com/golang 目录下已经有了 lint 也可以 copy 过来)

  6. `go install github.com/golang/lint/golint` 编译 golint

  7. 查看 gobin 目录下是否有了golint

解释：

解决方法是

使用终端切换到$GOPATH

按照下面目录结构来新建缺失的文件夹

<pre><code class="line-numbers">src
├── github.com
|      └── golang
└── golang.org
       └── x
</code></pre>

通过 `$ git clone git@github.com:golang/tools.git` 命令手动下载tools包

<pre><code class="language-go line-numbers">手动输入命令来安装失败的插件：
$ go install github.com/ramya-rao-a/go-outline
$ go install github.com/acroca/go-symbols
$ go install golang.org/x/tools/cmd/guru
$ go install golang.org/x/tools/cmd/gorename
...
</code></pre>

要能debug需要安装另外一个工具delve 。

安装方法见[链接][1]中找到对应的系统来安装delve工具。

[1]: https://github.com/derekparker/delve/blob/master/Documentation/installation/README.md