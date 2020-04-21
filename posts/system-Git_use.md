---
title: FF的Git使用整理
date: 2016-07-05 14:47:35
tags: [Git]
categories: [Git]
---
创建 Git仓库命令：(进入将要管理的Git文件夹地址下) git init
查看当前Git管理状态 git status
添加Git文件    git add *
提交文件到仓库 git commit  -m "加入注释"
推送文件到远程仓库     git push origin master
参考文章：<a href="http://www.bootcss.com/p/git-guide/" target="_blank" title="Git简易使用指南">Git简易使用指南</a> http://www.bootcss.com/p/git-guide/

### git 命令行常用命令


| git 作用 | 命令           |
| :---------- | :--------: |
| 检查更新状态      | git status |
|将文件添加进更新列表| git add * |
|commit 提交|git commit * -m "add some(not null非空)"|
|发布到服务器|use "git push" to publish your local commits|
|发布到主线 | git push origin master|
|发布tag release版本    |git tag |
|add tag  |git tag -m "first release" 0.1.0|
|git push |git push --tags|
| delete 远程tag |git push origin --delete tag|
| 检出远程分支文件 | git checkout -b dev origin/dev |
| 公钥加入本地ssh|ssh-add ~/.ssh/id_rse|
| 查看某域是否有ssh公钥，私钥|ssh -T git@git.oschina.net|


level 2

| git 作用     | 命令                                                         |
| ------------ | ------------------------------------------------------------ |
| 指定分支克隆 | git clone -b dev https://github.com/jinyuyoulong/Go-learn.git |
| 查询所有分支 | git branch -a                                                |

