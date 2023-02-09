---
title: Git 仓库
date: 2020-04-21
tags: [Git]
categories: [Git,system]
---

git 仓库的创建流程：

### 命令行模式创建 [参考](https://git-scm.com/book/zh/v2/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E5%9C%A8%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E6%90%AD%E5%BB%BA-Git)

1. 创建裸仓库 `git init --bare gitserver.git`，表明允许其副本push操作。

> 使用 `git init --bare <repo>` 可以创建一个裸仓库，当创建一个裸存储库时，Git假定裸存储库将作为几个远程用户的源存储库，因此它不会创建默认远程源。这意味着基本的git pull和git push操作将无法工作，因为Git假设没有工作空间，你不打算提交对裸存储库的任何更改。

> 从裸仓库 clone 下来的本地仓库可以进行正常的 `push` 操作， 但是从一般仓库 clone 下来的本地仓库却不行。 这也正是裸仓库存在的意义。 裸仓库一般情况下是作为远端的中心仓库而存在的。

git 创建裸仓库并修改该仓库目录的组权限为可写。

```sh
$ ssh user@git.example.com
$ cd /opt/git/my_project.git
$ git init --bare --shared
```

git clone 

```shell
git clone /Users/fanjinlong/dev/git/jdcrontab.git	
```



### gitea 工具创建

Gitea 是一个Go开发的开源Git管理工具。从Gogs项目中分裂出来，竟然是中国人无闻的项目（惊叹一下）。特点是：目标是打造一个最简单、最快速和最轻松的方式搭建自助 Git 服务。



### ssh 登录配置

参考 http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html

这时再输入下面的命令，将公钥传送到远程主机host上面：

> 　　$ ssh-copy-id user@host

好了，从此你再登录，就不需要输入密码了。

如果还是不行，就打开远程主机的/etc/ssh/sshd_config这个文件，检查下面几行前面"#"注释是否取掉。

> 　　RSAAuthentication yes
> 　　PubkeyAuthentication yes
> 　　AuthorizedKeysFile .ssh/authorized_keys

然后，重启远程主机的ssh服务。

> 　　// ubuntu系统
> 　　service ssh restart
>
> 　　// debian系统
> 　　/etc/init.d/ssh restart