---
title: mac下nvm 使用记录
tags:
  - nodejs
  - npm
  - nvm
id: 575
categories:
  - Nodejs
date: 2017-05-02 10:29:55
---

mac下nvm 使用记录
断开连接 brew unlink nvm
安装 brew install nvm
环境变量 add to ~/.bash_profile
export NVM_DIR="$HOME/.nvm"
. "$(brew --prefix nvm)/nvm.sh"
配置国内镜像源 export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/dist
配置npm镜像源
创建 ~/.npmrc 写入registry=https://registry.npm.taobao.org
更新环境变量 . ~/.bash_profile

查看可安装的nodejs版本 nvm ls-remote
安装node nvm install

删除版本 nvm uninstall v6
查看 nvm ls
切换nvm use //只针对当前shall
设置默认 nvm alias default v7

&nbsp;