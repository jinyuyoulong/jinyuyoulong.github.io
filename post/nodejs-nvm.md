---
title: nvm管理不同的node版本
tags: [nodejs,nvm]
categories: [Nodejs]
date: 2017-02-24 09:59:52
---

前任栽树后人乘凉 ：http://www.cnblogs.com/kongxianghai/p/5660101.html

### 安装多版本node

*   安装nvm
通过下面的命令可进行一步到位的安装，下面两种方式可二选一。
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash
或者:
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash

#### 安装

*   在命令行中运行命令，安装当前最新的稳定版。
`nvm install stable`
*   运行命令，指明版本，安装早期的版本0.12.4。
`nvm install 0.12.4`
*   安装后，当前使用的node版本默认为最后一次安装的版本，在命令行中运行命令可查看当前版本。
`nvm current`
*   切换node版本
`nvm use 6`
*   显示所有安装的版本
`nvm ls`
*   设置默认使用的版本
`nvm alias default version`

#### 卸载

*   删除引用
`nvm deactivate`
*   卸载
`nvm uninstall 7`

* * *

安装全局组件

非nvm管理的情况下，全局组件是安装到/usr/local/lib/node_modules下，然后通过软连接的方式把包中bin目录下的可执行文件链接到/usr/local/bin。不管用什么版本都装到这些目录下，多版本就没法玩了。

在nvm管理下，以沙箱的方式，全局组件会装到.nvm目录的当前版本node下，也就是装在nvm这个沙箱里，跟在指定版本的node下，当前有什么版本的node，就有对应的全局组件。这是nvm强大的地方，在多运行环境的管理和切换极为好用。

使用.nvmrc文件运行

在服务器上很多时候会运行多个应用系统，每个应用系统使用的node版本是不一样的，老系统用0.12.x甚至0.10.x，新系统用了新特新所以用最新的node版本，都很实际很正常。

为了让不同的应用系统使用各自所需的node版本运行，我们只需在各应用系统内的根目录里生成一个.nvmrc文件，在其内写一个版本号，利用nvm run &lt;系统启动文件>的方式运行系统，即可完成要求。**详情请看文章开头链接。**