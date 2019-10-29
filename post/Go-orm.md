---
title: Go orm 对比选择
date: 2019-07-10
categories:
  - Go
---

| name         | xorm  | gorm   |
| ------------ | ----- | ------ |
| github-stars | 5,053 | 14,262 |
| github-fork  | 650   | 1,606  |
|              |       |        |

xorm 自动生成代码

xorm help reverse

格式：xorm reverse dirver dbname 导出模板

```sh
xorm reverse mysql "username:pwd@tcp(127.0.0.1:3306)/dbname?charset=utf8" $GOPATH/src/github.com/go-xorm/cmd/xorm/templates/goxorm
```

