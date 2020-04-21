---
title: "Go 编译报错 expected 'IDENT', found 'go'"
author: fan
type: post
date: 2019-02-27T09:10:11+00:00
excerpt: 包的名字应只用小写。不要用下划线式，也不要用驼峰式。
url: /expected-ident-found-go/
categories:
  - Go
  - 其他技术
  - 错误集锦

---
#### 报错 expected &#8216;IDENT&#8217;, found &#8216;go&#8217;

运行go run
  
文件目录为

<pre><code class="language-shell line-numbers">.
├── README.md
├── fetch
│   ├── fetch.go
│   ├── fetch1.7.go
│   ├── fetchall.go
│   ├── server1.go
│   ├── server2.go
│   └── server3.go
└── go-demo
    ├── main.go
    ├── mgif.go
    └── mutiFiles-package
        ├── main.go
        └── util.go
</code></pre>

./go-demo/main.go

<pre><code class="language-go line-numbers">package go-demo
...
</code></pre>

由于package 命名为go-demo，命名格式不规范，导致的这个问题。
  
解决办法：将go-demo 统一改为 gostart ，去掉 `-` 字符 报错解决。
  
反思：包的名字应只用小写。不要用下划线式，也不要用驼峰式。使用单数
  
参考: https://studygolang.com/articles/11823