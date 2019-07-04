---
title: docker 安装并使用Redis
data: 2019-06-07
---

docker 安装并使用Redis

1. docker search redis

2. docker pull redis #获得的是lasted版本 redis:3.2

3. 配置redis 

   ```sh
   mkdir -p ./docker/redis/data
   mkdir -p ./docker/redis/conf
   vi redis.conf
   ```

4. ```sh
   # redis.conf
   bind 127.0.0.1
   protected-mode yes
   appendonly no//持久化
   # requirepass foobared
   ```

   

ps
protected-mode 是在没有显示定义 bind 地址（即监听全网断），又没有设置密码 requirepass
时，只允许本地回环 127.0.0.1 访问。 也就是说当开启了 protected-mode 时，如果你既没有显示的定义了 bind
监听的地址，同时又没有设置 auth 密码。那你只能通过 127.0.0.1 来访问 redis 服务