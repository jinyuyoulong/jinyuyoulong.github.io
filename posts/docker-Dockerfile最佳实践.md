---
title: "System Dockerfile最佳实践"
date: 2019-05-05T13:44:44+08:00
categories: [Docker]
---
Dockerfile入门之后面临一个问题：如何在实际的开发过程中正确配置 Dockerfile？

Dockerfile 有两个方向上的使用方式：

  1. 只用 Dockerfile 管理镜像
  2. <ol start="2">
      <li>
        使用docker-compose 容器编排技术 共同管理镜像的 build。<br /> 下面是我对Dockerfile最佳实践的总结：<br /> 共同遵守的原则:
      </li>

    </ol>

一个容器只负责做一件事情。

保持常见的指令像 MAINTAINER 以及从上至下更新 Dockerfile 命令。

当构建镜像时使用可理解的标签，以便更好地管理镜像。

避免在 Dockerfile 中映射公有端口。

CMD 与 ENTRYPOINT 命令请使用数组语法。

针对一：只用 Dockerfile 管理镜像的 build
<<<<<<< HEAD:posts/2019-05-08-dockerfile最佳实践.md
=======
```dockerfile
# 依赖最小Linux环境 alpine 只用5M大小
FROM alpine
>>>>>>> 9b93207d813e2b213031f967612e37c68194cf37:posts/docker-Dockerfile最佳实践.md

<pre><code class="language-dockerfile line-numbers"># 依赖最小Linux环境 alpine 只用5M大小
FROM alpine
# MAINTAINER：设置该镜像的作者。
MAINTAINER jinlong
# 将当前目录下的所有文件都拷贝进入 image 文件的/app目录
COPY ./bin/ /app
# 指定接下来的工作路径为/app
# WORKDIR：指定RUN、CMD与ENTRYPOINT命令的工作目录。
# 所有下面的 RUN 命令都在 WORKDIR 目录下面执行
WORKDIR /app
# RUN：在shell或者exec的环境下执行的命令。RUN指令会在新创建的镜像上添加新的层面，接下来提交的结果用在Dockerfile的下一条指令中。
#RUN cd bin/
<<<<<<< HEAD:posts/2019-05-08-dockerfile最佳实践.md
# ADD：复制文件指令。它有两个参数&lt;source&gt;和&lt;destination&gt;。destination是容器内的路径。source可以是URL或者是启动配置上下文中的一个文件。
# ADD 《src》 《destination》
# CMD：提供了容器默认的执行命令。 Dockerfile只允许使用一次CMD指令。 使用多个CMD会抵消之前所有的指令，只有最后一个指令生效。 CMD有三种形式：
=======

# ADD：复制文件指令。它有两个参数<source>和<destination>。
# destination是容器内的路径。
# source可以是URL或者是启动配置上下文中的一个文件。
# ADD 《src》 《destination》


# CMD：提供了容器默认的执行命令。 Dockerfile只允许使用一次CMD指令。 使用多个CMD会抵消之前所有的指令，只有最后一个指令生效。 
# CMD有三种形式：
>>>>>>> 9b93207d813e2b213031f967612e37c68194cf37:posts/docker-Dockerfile最佳实践.md
#CMD ["executable","param1","param2"]
#CMD ["param1","param2"]
#CMD command param1 param2
#CMD ./gin
CMD ["./gin"]
#-------------
# 开放端口 永远都不要在这里使用端口映射，这违反了可移植性
# EXPOSE：指定容器在运行时监听的端口。
# private and public mapping
# EXPOSE 80:8080
# ENTRYPOINT：配置给容器一个可执行的命令
# 这意味着在每次使用镜像创建容器时一个特定的应用程序可以被设置为默认程序。同时也意味着该镜像每次被调用时仅能运行指定的应用。类似于CMD
# ENTRYPOINT ["executable", "param1","param2"]
# ENV：设置环境变量。它们使用键值对，增加运行程序的灵活性。
# ENV &lt;key&gt; &lt;value&gt;
# USER：镜像正在运行时设置一个UID。语法如下
# USER &lt;uid&gt;
# VOLUME：授权访问从容器内到主机上的目录。
# VOLUME ["/data"]
<<<<<<< HEAD:posts/2019-05-08-dockerfile最佳实践.md
</code></pre>
=======
```

## 有UI界面portainer，用什么命令行，SB

好了安装portainer 镜像管理镜像吧。

```sh
$ docker volume create portainer_data
$ docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

over.

>>>>>>> 9b93207d813e2b213031f967612e37c68194cf37:posts/docker-Dockerfile最佳实践.md
