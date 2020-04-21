---
title: thinkphp5之SQL
author: fan
type: post
date: 2019-01-16T03:27:54+00:00
url: /thinkphp5之sql/
categories:
  - PHP

---
* * *title: tp5</p> 

## date: 2018-12-18

<pre><code class="language-mysql line-numbers">    # 表达式   不区分大小写，
    # EQ    =
    # NEQ   &lt;&gt;  不等于
    # LT    &lt;
    # ELT   &lt;=
    # RT    &gt;
    # ELT   &gt;=
    # BETWEEN   BETWEEN * AND *
    # NOTBETWEEN    NOTBETWEEN * AND *
    # IN    IN (*,*)
    # NOTIN NOT IN (*,*)
</code></pre>

`$sql = $db->where('id','between',"1,5")->buildSql();`