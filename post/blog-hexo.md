---
title: 使用hexo的第一篇文章
date: 2016-06-30 17:40:48
tags: 
  - hexo
categories:
  - blog
---
### hexo建站之后如何使用
#### 1.如何写文章
hexo 需要配合git使用
创建文章：需要在terminal 输入命令 hexo new "文章名"
创建好的"文件名.md" 文件会放在站点目录 ./source/_posts/ 下

注意：资源文件都放在source/_posts文件下（不要创建其他目录，否则解析的时候可能会报错）

#### 2.如何发布文章
每次发布文章都需要执行命令：

hexo generate

hexo deploy

####  3.本地启动hexo 查看网站更新
hexo server

#### 4.设置新建文章的模板

创建新文件: hexo new passageName

默认创建在source/_post目录下，使用scaffolds/post.md作为模板

文章filename根据_config.yml配置自动创建为new_post_name: :year-:month-:day-:title.md