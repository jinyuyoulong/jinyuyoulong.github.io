---
  title: docker 使用规则
  tags: [Docker]
  categories: [ 操作系统,Docker]
date: 2018-04-04 09:39:10
---
[TOC]
## 硬件/操作系统 要求
Docker支持以下的发行版版本：

- Ubuntu18.04 LTS 是目前对docker兼容性最好的发行版

- CentOS 7 (64-bit)，要求内核版本不低于 3.10 。CentOS 7 满足最低内核的要求，但由于内核版本比较低，部分功能（如 `overlay2` 存储层驱动）无法使用，并且部分功能可能不太稳定。
- Debain 9

------

## 前提条件

目前，CentOS 仅发行版本中的内核支持 Docker。

Docker 运行在 CentOS 7 上，要求系统为64位、系统内核版本为 3.10 以上。

Docker 运行在 CentOS-6.5 或更高的版本的 CentOS 上，要求系统为64位、系统内核版本为 2.6.32-431 或者更高版本。

  ### docker 的组件结构

  Docker 由镜像(Image)、容器(Container)、仓库(Repository) 三部分组成。

  docker-machine, docker, docker-compose (docker环境)

  docker container 容器(运行实例)

  docker image 镜像(安装实例)

  Dockerfile(用于生成image)

  ### docker配置+使用

  预先安装docker的相关库
  ```
  brew install 
  docker
  docker-compose
  docker-machine
  ```

#### 关于 docker-machine 

[Docker Machine](https://docs.docker.com/machine/overview/) 是 Docker 官方提供的一个工具，它可以帮助我们在远程的机器上安装 Docker，或者在虚拟机 host 上直接安装虚拟机并在虚拟机中安装 Docker。我们还可以通过 docker-machine 命令来管理这些虚拟机和 Docker。

Mac 命令行安装 docker的话需要首先安装 docker-machine,默认启动的虚拟机对外IP：192.168.99.100

`tcp://192.168.99.100:2376`

  #### 启动docker-machine 

  To have launchd start docker-machine now and restart at login:
   `brew services start docker-machine`

  Or, if you don't want/need a background service you can just run:
  `docker-machine start`

  ### 利用docker-machine 使 docker从创建到启动步骤

---

  1. docker-machine ls 	//检查docker-machine 是否启动了,如果查看的URL为空，则启动docker-machine 

  1. docker-machine start 或 docker-machine create default // 启动或创建docker虚拟主机。每一次启动都要重新创建，默认为 default。
  2. docker-machine env	//配置docker 虚拟主机环境变量
  3. eval $(docker-machine env)	// 使default环境变量生效

---
  docker操作
  5. docker image pull ubuntu // 拉取镜像库

  6. docker image ls // 查看 已经安装的 image 镜像

  7. docker container run ubuntu //命令会从 image 文件，生成一个正在运行的容器实例。

  8. docker exec -it [容器ID] bash //进入已运行的容器，进行bash操作

  ### docker 使用规则

  镜像源：https://www.docker-cn.com/registry-mirror
  在docker或网易蜂巢的镜像库中找到需要的image
  docker pull hub.c.163.com/library/mysql:latest
  docker images
  //启动容器,端口映射8888:8080 
  docker run -b -p 8888:8080 hub.c.163.com/library/mysql 

  `docker container run hello-world`

  输出这段提示以后，`hello world`就会停止运行，容器自动终止。

  有些容器不会自动终止，因为提供的是服务。比如，安装运行 Ubuntu 的 image，就可以在命令行体验 Ubuntu 系统。

  `docker container run -it ubuntu bash`

  ### 编写 Dockerfile 文件生成image
  1. 新建 .dockerignore 文件
     写入要忽略的目录/文件

  ```
  .git
  node_modules
  npm-debug.log
  ```
  2. 新建文本文件 Dockerfile

Dockerfile 是一个文本文件，其内包含了一条条的 **指令(Instruction)**，每一条指令构建一层，因此每一条指令的内容，就是描述该层应当如何构建。

  写入环境配置

  ```dockerfile
  FROM node:8.4 //该 image 文件继承官方的 node image，冒号表示标签，这里标签是8.4，即8.4版本的 node。
  COPY . /app	//将当前目录下的所有文件（除了.dockerignore排除的路径），都拷贝进入 image 文件的/app目录。
  WORKDIR /app	//指定接下来的工作路径为/app。
  RUN npm install --registry=https://registry.npm.taobao.org	//在/app目录下，运行npm install命令安装依赖。注意，安装后所有的依赖，都将打包进入 image 文件。
  EXPOSE 3000	//将容器 3000 端口暴露出来， 允许外部连接这个端口。
  CMD node demos/01.js	//容器启动后自动执行node demos/01.js。
  ```

  3. 创建 image 文件

  `docker image build -t koa-demo .` 或` docker image build -t koa-demo:0.0.1 .` 

`docker build` 命令最后有一个 `.`。`.` 表示当前目录，而 `Dockerfile` 就在当前目录，因此不少初学者以为这个路径是在指定 `Dockerfile` 所在路径，这么理解其实是不准确的。如果对应上面的命令格式，你可能会发现，这是在指定 **上下文路径**。

  4. 生成容器

  `docker container run -p 8000:3000 -it koa-demo /bin/bash`

  ### 发布 image 文件

  去 hub.docker.com 或 cloud.docker.com 注册一个账户.
  1. docker login
  2. 为本地的 image 标注用户名和版本。
  3. 重新构建一下 image 文件。
  4. 发布 image 文件。
  5. 发布成功以后，登录 hub.docker.com，查看已经发布的 image 文件。

  ### 其他docker命令

  ```sh
  docker-machine env 	// 查看环境变量：IP
  docker ps 					//查看运行的docker
  netstat -na|grep 8888 // 查看端口监听情况
  docker exec -it [容器ID] bash //进入容器，进行bash操作 -it：这是两个参数，一个是 -i 表示交互式操作，一个是 -t 为终端。
  docker run -ti -d --name my-nginx -p 8088:80 docker.io/nginx // 端口映射
  docker rm containerId // 删除 容器文件
  docker rmi imageId 		// 删除 image文件
  docker stop 1f 				// 停止运行的容器
  docker start 					//启动一个或多个已经被停止的容器
  docker stop 					//停止一个运行中的容器
  docker restart b0				//重启容器
  docker container kill [containID] // 手动终止 运行的 容器
  docker container ls 	// 列出本机正在运行的容器
  docker container ls --all //列出本机所有容器，包括终止运行的容器
  docker volume create portainer_data
  
  ```
  docker-machine create default // 创建docker虚拟主机，每一次启动都要重新创建，默认创建环境名为 default。如果报错，boot2docker.iso 无法下载可以在GitHub上单独下载后放到 /Users/$username/.docker/machine/cache/ 下

  在容器的命令行，按下 Ctrl + c 停止 Node 进程，然后按下 Ctrl + d （或者输入 exit）退出容器。

#### Docker的数据持久化主要有两种方式：

- bind mount
- volume

**使用volume**

volume也是绕过container的文件系统，直接将数据写到host机器上，只是volume是被docker管理的，docker下所有的volume都在host机器上的指定目录下/var/lib/docker/volumes。

将my-volume挂载到container中的/mydata目录：

```
docker run -it -v my-volume:/mydata alpine sh
```



#### /var/run/docker.sock文件
这个文件是什么呢？为什么有些容器需要使用它？简单地说，它是Docker守护进程(Docker daemon)默认监听的Unix域套接字(Unix domain socket)，容器中的进程可以通过它与Docker守护进程进行通信。

Portainer镜像通过绑定的/var/run/docker.sock文件与**Docker守护进程**通信，执行各种管理操作。

  #### 一些使用原则

  1. *在创建 Docker Image 的时候使用 **-t** 参数对 Image 打上 Tag*

  2. *不要在 Dockerfile 中进行端口映射*

  如果 Image 的使用者关心 Container 应该将自己的什么端口和 host 的端口进行映射，那就会显式地在创建 Container 的时候使用 **-p** 参数进行设置，否则，Docker 会自动给 Container 分配一个 host 上的端口进行映射。

  3. 在使用 **CMD** 和 **ENTRYPOINT** 指示的时候使用数组传入参数 `CMD ["/bin/echo"]`
  4. **CMD **和 **ENTRYPOINT** 最好配合使用

  **注意**

  docker是运行在Linux上的，在Windows/Mac中运行docker，实际上还是在Windows/Mac下先安装了一个Linux环境，然后在这个系统中运行的docker。也就是说，服务中使用的localhost指的是这个Linux环境的地址，而不是我们的宿主环境Windows/Mac。我们可以通过命令：`docker-machine ip default`

  **找到这个Linux的ip地址，一般情况下这个地址是192.168.99.100，然后在 Windows/Mac 的浏览器中，输入这个地址，加上服务的端口即可启用了。** `http://192.168.99.100:8080`

  ### docker-compose 编排项目

  docker-compose build 	//编排 image

  docker-compose run my-gin //创建并启动容器

  docker-compose.yml	//配置文件

  ```yaml
version: "2"
services:
  gili-api:
    image: gili-api:latest
    restart: always
    environment:
      MYSQL_DSN: "root:K3b4XRqsmVpW@tcp(172.20.0.2)/giligili?charset=utf8&parseTime=True&loc=Local"
      REDIS_ADDR: "172.21.0.2:6379"
      REDIS_PW: ""
      REDIS_DB: "0"
      SESSION_SECRE: "K3b4XRqsmVpW"
      GIN_MODE: "release"
    ports:
      - 3002:3000
  mysql:
    image: mysql:5.6
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: K3b4XRqsmVpW
    volumes:
      - mysql_data:/var/lib/mysql/data
    ports:
      - 3306:3306

  redis:
    container_name: redis
    image: redis
    restart: always
    ports:
      - 6379:6379

  ```



**在docker容器里localhost并不是指宿主机的localhost**

由此原因，并不能在容器中通过localhost:3306访问到宿主机的mysql

**docker在运行时就建立了虚拟网卡，并命名为docker0**

我们可以在宿主机上运行ifconfig看到它，这就是宿主机建立的网桥，用于与各个容器之间通信

 **宿主机在与容器同一局域网的IP地址一般是docker0对应的IP地址段的首个地址（如172.0.17.1）**

我们可以在容器里通过172.0.17.1:3306访问到宿主机的mysql服务器

ip 查询命令：`ip addr show`

  [Docker 入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)

  [Docker 微服务教程](http://www.ruanyifeng.com/blog/2018/02/docker-wordpress-tutorial.html)

  [Dockerfile 最佳实践](https://studygolang.com/articles/4219)

https://registry.docker-cn.com

https://yeasy.gitbooks.io/docker_practice/