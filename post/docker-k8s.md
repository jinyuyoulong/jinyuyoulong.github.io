---
title: k8s在Mac上的安装和使用
date: 2019-07-08
categories: [Docker]
tags: [k8s,kubernetes,Docker]
---

# 安装

在Mac下安装前提条件，已经安装好了docker desktop，并修改了代理源 https://registry.docker-cn.com。

直接在docker桌面端开启k8s是没用的，一直提示 kubernetes is starting… :cry: 我竟然不知道，这样子持续了n天。​



## 自己手动编译安装 k8s

- git clone https://github.com/maguowei/k8s-docker-for-mac.git

- cd k8s-docker-for-mac/

- ./load_images.sh





## 安装minikube

```sh
# install minikube
$ brew cask install minikube
$ brew install docker-machine-driver-xhyve
# docker-machine-driver-xhyve need root owner and uid
$ sudo chown root:wheel $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
$ sudo chmod u+s $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
```

最后启动minikube

```sh
# start minikube.
# http proxy is required in China
$ minikube start --docker-env HTTP_PROXY=http://proxy-ip:port --docker-env HTTPS_PROXY=http://proxy-ip:port --vm-driver=xhyve
```



## Ubuntu

安装 kubeadm kubectl kubelet 三个包