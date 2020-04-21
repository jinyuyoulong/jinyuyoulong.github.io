---
title: Go交叉编译
author: fan
type: post
date: 2019-04-18T09:25:29+00:00
url: /go交叉编译/
categories:
  - Go
  - Mac
  - 操作系统

---
查看操作系统平台和内核版本：`uname -a`
  
Mac 下编译 Linux 和 Windows 64位可执行程序

<pre><code class="language-shell line-numbers">CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
</code></pre>

Linux 下编译 Mac 和 Windows 64位可执行程序

<pre><code class="language-shell line-numbers">CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
</code></pre>

Windows 下编译 Mac 和 Linux 64位可执行程序

<pre><code class="language-shell line-numbers">SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build main.go
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go
</code></pre>

Mac 编译 Linux 32位可执行程序

<pre><code class="language-shell line-numbers">CGO_ENABLED=0 GOOS=linux GOARCH=386 go build main.go
</code></pre>

CGO_ENABLED = 0 交叉编译不支持 CGO 所以要禁用它。
  
GOOS：目标平台的操作系统（darwin、freebsd、linux、windows）
  
GOARCH：目标平台的体系架构（386、amd64、arm）
  
CGO是一个令人惊异的技术，它允许Go与C的类库交互操作，让Go能够使用 C语言 积累的各种资源。
  
对于使用CGO的程序，大部分情况可以通过配置$CC参数使用自行准备的交叉编译工具进行编译。

<pre><code class="language-shell line-numbers">CGO_ENABLED=1 GOOS=linux GOARCH=arm CC=/Volumes/Armx/bin/arm-none-linux-gnueabi-gcc GOARM=5 go build -x main.go
</code></pre>

其中$CC参数指定的是ARM工具链位置。
  
目前解决CGO跨平台编译问题的思路有：
  
&#8211; 用目标平台的工具链进行交叉编译
  
&#8211; 用原生代码重写CGO实现的功能，当然这是一句废话:small: