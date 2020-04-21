---
title: WordPress4.4之后原生支持REST API
tags: [WordPress]
categories: [blog]
date: 2018-04-10 05:33:11
---

WordPress4.4之后REST API 格式:www.网址/wp-json/wp/v2,例：`www.v5u.win/wp-json/wp/v2` 路由参数有五个，posts,pages,categories,tags,comments。 例：`www.v5u.win/wp-json/wp/v2/posts` url参数有： per_page(每页记录数)， page(页码), orderby(排序规则), order(排序方式) 例：`?per_page=8&page=1&orderby=date&order=desc`每页显示8条，第一页，以时间排序，降序展示。 官方文档REST API在这里查看： https://developer.wordpress.org/rest-api/