---
title: tp5 db
date: 2018-12-18
---

```mysql
    # 表达式   不区分大小写，
    # EQ    =
    # NEQ   <>	不等于
    # LT    <
    # ELT   <=
    # RT    >
    # ELT   >=
    # BETWEEN   BETWEEN * AND *
    # NOTBETWEEN    NOTBETWEEN * AND *
    # IN    IN (*,*)
    # NOTIN NOT IN (*,*)
```
`$sql = $db->where('id','between',"1,5")->buildSql();`

