---
title: Go orm 对比选择
date: 2019-07-10
categories: [Go]
---

golang 中 orm最主流的两个包，xorm和gorm。所以主要在他们之间做抉择。

| name         | xorm  | gorm   |
| ------------ | ----- | ------ |
| github-stars | 5,053 | 14,262 |
| github-fork  | 650   | 1,606  |
|              |       |        |

不管是从stars数还是fork gorm都是大比例拉开。gorm是老牌的项目，xorm是这两年崛起来的。

最后我选择了xormplus 因为路径依赖，学习golang的时候的示例用的是xorm。:sweat_smile:

xorm 自动生成代码

xorm help reverse

格式：xorm reverse dirver dbname 导出模板

```sh
xorm reverse mysql "username:pwd@tcp(127.0.0.1:3306)/dbname?charset=utf8" $GOPATH/src/github.com/go-xorm/cmd/xorm/templates/goxorm
```

