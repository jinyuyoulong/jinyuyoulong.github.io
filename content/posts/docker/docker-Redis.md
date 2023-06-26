---
title: docker 安装并使用Redis
date: 2019-06-07
categories: [Docker]
tags: [Docker]
---

docker 安装并使用Redis

1. docker search redis

2. docker pull redis #获得的是lasted版本 redis:3.2

3. 配置redis 

```sh
   mkdir -p /root/redis/data
   mkdir -p /root/redis/conf
   vi redis.conf
```

```sh
   # redis.conf
   bind 127.0.0.1
   protected-mode yes
   appendonly no//持久化
   # requirepass foobared
```

   

p.s.
protected-mode 是在没有显示定义 bind 地址（即监听全网断），又没有设置密码 requirepass
时，只允许本地回环 127.0.0.1 访问。 也就是说当开启了 protected-mode 时，如果你既没有显示的定义了 bind
监听的地址，同时又没有设置 auth 密码。那你只能通过 127.0.0.1 来访问 redis 服务

4. 启动redis

命令行启动 `docker run -p 6379:6379 --name myredis  -d redis`

5. 测试或debug

```sh
# 查看活跃的容器
docker ps
# 如果没有 myredis 说明启动失败 查看错误日志
docker logs myredis
# 查看 myredis 的 ip 挂载 端口映射等信息
docker inspect myredis
# 查看 myredis 的端口映射
docker port myredis	
```
redis 简单使用
进入后台操作系统：redis-cli

```sh
$redis-cli
redis 127.0.0.1:6379>
redis 127.0.0.1:6379> PING

PONG
```