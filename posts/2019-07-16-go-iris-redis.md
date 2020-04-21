---
title: Go Iris Redis
author: fan
type: post
date: 2019-07-16T05:43:58+00:00
url: /go-iris-redis/
categories:
  - Go
tags:
  - Go

---
[TOC]

# iris 中使用 Redis

iris 内置对 Redis 的支持，但是她和 session 结合的比较紧密，比如每一个方法传参都大部分都有 sid，在当前文件 database.go 找了半天没找到在哪里定义了 sid，`func (db *Database) Get(sid string, key string) (value interface{})`
  
只能推断是 sessionId，果然在 Session struct 中发现了 sid。

<pre><code class="language-go line-numbers">Session struct {
        sid      string
        isNew    bool
        flashes  map[string]*flashMessage
        mu       sync.RWMutex // for flashes.
        Lifetime LifeTime
        provider *provider
    }
</code></pre>

所以可以下结论，iris中必须使用内置的 Redis 是只对 session 的配合支持，如果需要单独操作 Redis 数据库，则需要使用其他的第三方库来操作，比如：redigo 和 go-redis/redis