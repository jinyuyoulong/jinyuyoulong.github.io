---
  title: docker 使用规则
  tags:
    - docker
  categories:
    - 操作系统
date: 2018-04-04 09:39:10
---
## 硬件/操作系统 要求
Docker支持以下的CentOS版本：

- CentOS 7 (64-bit)
- CentOS 6.5 (64-bit) 或更高的版本

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

  #### 启动docker-machine

  To have launchd start docker-machine now and restart at login:
   `brew services start docker-machine`

  Or, if you don't want/need a background service you can just run:
  `docker-machine start`

  ### docker从创建到启动步骤

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
  2. 新建文本文件Dockerfile

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

  ```
  docker-machine env // 查看环境变量：IP
  docker ps //查看运行的docker
  netstat -na|grep 8888 // 查看端口监听情况
  docker exec -it [容器ID] bash //进入容器，进行bash操作 -it：这是两个参数，一个是 -i 表示交互式操作，一个是 -t 为终端。
  docker run -ti -d --name my-nginx -p 8088:80 docker.io/nginx // 端口映射
  docker rm containerId // 删除 容器文件
  docker rmi imageId // 删除 image文件
  docker stop 1f // 停止运行的容器
  docker start :启动一个或多个已经被停止的容器
  docker stop :停止一个运行中的容器
  docker restart :重启容器
  docker container kill [containID] // 手动终止 运行的 容器
  docker container ls // 列出本机正在运行的容器
  docker container ls --all //列出本机所有容器，包括终止运行的容器
  ```
  docker-machine create default // 创建docker虚拟主机，每一次启动都要重新创建，默认创建环境名为 default。如果报错，boot2docker.iso 无法下载可以在GitHub上单独下载后放到 /Users/$username/.docker/machine/cache/ 下

  在容器的命令行，按下 Ctrl + c 停止 Node 进程，然后按下 Ctrl + d （或者输入 exit）退出容器。

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
  version: '3'
  services:

    my-gin:
      build: .
      image: my-gin:v5
      ports:
       - "7070:7070"
      container_name: goweb
      hostname: web
  ```

  [Docker 入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)

  [Docker 微服务教程](http://www.ruanyifeng.com/blog/2018/02/docker-wordpress-tutorial.html)

  [Dockerfile 最佳实践](https://studygolang.com/articles/4219)