---
title: React-Native 初次安装环境报错及解决记录
tags: [ReactNative]
categories: [iOS]
date: 2016-03-15 16:38:19
---

创建第一个项目后，打开xcode运行，terminal报错

Watchman:  watchman--no-pretty get-sockname returned with exit code null dyld: Library not loaded: /usr/local/opt/pcre/lib/libpcre.1.dylib

        解决方案：终端输入 brew link pcre，
        如果报错没有写入权限（Could not symlink lib/libpcre.1.dylib
        /usr/local/lib is not writable.）
        则授权给该文件 sudo chown -R $(whoami) /usr/local/lib
    