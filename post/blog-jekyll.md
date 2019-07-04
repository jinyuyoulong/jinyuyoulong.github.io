---
title: jekyll using standards 使用规范
categories: 
- blog
tags:
  - jekyll
date: 2016-9-3 15:47:05
---

## <center>jekyll using standards 使用规范<center/>

1. 文章就是普通的文本文件，文件名假定为2012-08-25-hello-world.html。
   (注意，文件名必须为"年-月-日-文章标题.后缀名"的格式。如果网页代码采用html格式，后缀名为html；如果采用markdown格式，后缀名为md。）

2. 在该文件中，填入以下内容：（注意，行首不能有空格）

```
    ---
	layout: default
	title: 你好，世界
	---
	<h2>{{ page.title }}</h2>
	<p>我的第一篇文章</p>
    <p>{{ page.date | date_to_string }}</p>
　　
```
3. 每篇文章的头部，必须有一个yaml文件头，用来设置一些元数据。
   它用三根短划线"---"，标记开始和结束，里面每一行设置一种元数据。"layout:default"，表示该文章的模板使用_layouts目录下的default.html文件；"title: 你好，世界"，表示该文章的标题是"你好，世界"，
   如果不设置这个值，默认使用嵌入文件名的标题，即"hello world"。

   每个页面都可以有自己的头信息，可以覆盖Jekyll和_config.yml里面的值

   ```
   ---
   layout: post
   title: 一步一步创建Jekyll主题
   categories: [jekyll github markdown rouge]
   date: 2016-9-3 15:47:05
   excerpt: ""   # 覆盖清掉文章的摘要
   pid: ""       # 新建一个pid的字符串变量
   ---
   ```

   

4. 使用模板变量

```
	在yaml文件头后面，就是文章的正式内容，里面可以使用模板变量。	{{ page.title }}就是文件头中设置的"你好，世界"，	{{ page.date }}则是嵌入文件名的日期（也可以在文件头重新定义date变量），"| date_to_string"表示将page.date变量转化成人类可读的格式。
```
5. 发布

   正常的git管理发布

`ps: 本地也需要安装builder工具，so 那为什么不用hexo？`

文章参考: 

[阮一峰的网络日志](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)

[一步一步创建Jekyll主题](http://gitgj.oschina.io/2016/09/03/how-to-create-the-jekyll-theme.html)

