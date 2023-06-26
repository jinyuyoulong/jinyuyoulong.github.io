---
title: "V2ray记录"
date: 2021-05-24T19:04:35+08:00
toc: true
tags: [翻墙]
categoryies: [system]
---
[TOC]

v2ray是什么？
v2是继小飞机ss之后的下一个技术方案。（不能明说）
v2 的优点：转发容易，匿名性高，可多级代理转发。
v2的缺点：配置相对复杂，客户端生态不完善。
下面从安装+使用，两个方面总结。
[TOC]
参考https://toutyrater.github.io/basic/vmess.html
环境建议：使用debain9，Ubuntu 16以上，不推荐centos

## 安装

wget https://install.direct/go.sh
bash go.sh
或
bash <(curl -s -L https://install.direct/go.sh)

## 配置

vi /etc/v2ray/config.json

## 启动

sudo systemctl start v2ray
在首次安装完成之后，V2Ray 不会自动启动，需要手动运行上述启动命令。而在已经运行 V2Ray 的 VPS 上再次执行安装脚本，安装脚本会自动停止 V2Ray 进程，升级 V2Ray 程序，然后自动运行 V2Ray。在升级过程中，配置文件不会被修改。
对于安装脚本，还有更多用法，在此不多说了，可以执行 bash go.sh -h 看帮助。
使用
service v2ray start
service v2ray status
有时候无法连接Google ，服务器没有问题，需要重启一下客户端。
客户端 列表
https://www.v2ray.com/awesome/tools.html
安装后的显示信息：

```
Extracting V2Ray package to /tmp/v2ray.
Archive:  /tmp/v2ray/v2ray.zip
  ...
PORT:123456
UUID:xxx
Updating software repo
Installing daemon
```
centos6 问题解决 uninstall daemon & systemctl not found
因为 centos6没有 systemctl 并且，v2ray不支持 centos6
https://hellojxl.com/2018/07/27/v2ray%E5%AE%89%E8%A3%85%E6%B3%A8%E6%84%8F%E8%AE%B0%E5%BD%95/
开机启动

```
    vi /etc/init.d/v2ray
    #!/bin/sh
    #
    # v2ray        Startup script for v2ray
    #
    # chkconfig: - 24 76
    # processname: v2ray
    # pidfile: /var/run/v2ray.pid
    # description: V2Ray proxy services
    #
    ### BEGIN INIT INFO
    # Provides:          v2ray
    # Required-Start:    $network $local_fs $remote_fs
    # Required-Stop:     $remote_fs
    # Default-Start:     2 3 4 5
    # Default-Stop:      0 1 6
    # Short-Description: V2Ray proxy services
    # Description:       V2Ray proxy services
    ### END INIT INFO
    DESC=v2ray
    NAME=v2ray
    DAEMON=/usr/bin/v2ray/v2ray
    PIDFILE=/var/run/$NAME.pid
    LOCKFILE=/var/lock/subsys/$NAME
    SCRIPTNAME=/etc/init.d/$NAME
    RETVAL=0
    DAEMON_OPTS="-config /etc/v2ray/config.json"
    # Exit if the package is not installed
    [ -x $DAEMON ] || exit 0
    # Read configuration variable file if it is present
    [ -r /etc/default/$NAME ] && . /etc/default/$NAME
    # Source function library.
    . /etc/rc.d/init.d/functions
    start() {
      local pids=$(pgrep -f $DAEMON)
      if [ -n "$pids" ]; then
        echo "$NAME (pid $pids) is already running"
        RETVAL=0
        return 0
      fi
      echo -n $"Starting $NAME: "
      mkdir -p /var/log/v2ray
      $DAEMON $DAEMON_OPTS 1>/dev/null 2>&1 &
      echo $! > $PIDFILE
      sleep 2
      pgrep -f $DAEMON >/dev/null 2>&1
      RETVAL=$?
      if [ $RETVAL -eq 0 ]; then
        success; echo
        touch $LOCKFILE
      else
        failure; echo
      fi
      return $RETVAL
    }
    stop() {
      local pids=$(pgrep -f $DAEMON)
      if [ -z "$pids" ]; then
        echo "$NAME is not running"
        RETVAL=0
        return 0
      fi
      echo -n $"Stopping $NAME: "
      killproc -p ${PIDFILE} ${NAME}
      RETVAL=$?
      echo
      [ $RETVAL = 0 ] && rm -f ${LOCKFILE} ${PIDFILE}
    }
    reload() {
      echo -n $"Reloading $NAME: "
      killproc -p ${PIDFILE} ${NAME} -HUP
      RETVAL=$?
      echo
    }
    rh_status() {
      status -p ${PIDFILE} ${DAEMON}
    }
    # See how we were called.
    case "$1" in
      start)
        rh_status >/dev/null 2>&1 && exit 0
        start
        ;;
      stop)
        stop
        ;;
      status)
        rh_status
        RETVAL=$?
        ;;
      restart)
        stop
        start
        ;;
      reload)
        reload
      ;;
      *)
        echo "Usage: $SCRIPTNAME {start|stop|status|reload|restart}" >&2
        RETVAL=2
      ;;
    esac
    exit $RETVAL
```

## 增加权限并加入开机启动

```
    chmod a+x /etc/init.d/v2ray
    chkconfig v2ray on
    service v2ray start
```