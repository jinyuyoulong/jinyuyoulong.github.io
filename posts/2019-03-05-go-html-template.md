---
title: Go HTML template
author: fan
type: post
date: 2019-03-05T09:47:46+00:00
url: /go-html-template/
categories:
  - Go
tags:
  - Go

---
<pre><code class="language-go line-numbers">文档
go doc text/template
$ go doc html/template
</code></pre>

### 应用

<pre><code class="language-go line-numbers">&lt;br />func main() {
    // 定义模板显示格式
    const templ = `A: {{.A}}
&lt;p&gt;B: {{.B}}&lt;/p&gt;`
    // 模板配置函数
    t := template.Must(template.New("escape").Parse(templ))
    var data struct {
        A string        // untrusted plain text
        B template.HTML // trusted HTML
    }
    // A是一个普通字符串，B是一个信任的template.HTML字符串类型。
    data.A = "&lt;b&gt;Hello!&lt;/b&gt;"
    data.B = "&lt;b&gt;Hello!&lt;/b&gt;"
    // 使用定义好的 模板 输出到 控制台
    if err := t.Execute(os.Stdout, data); err != nil {
        log.Fatal(err)
    }
}
/*
autoescape.html 结果
A:&lt;b&gt;Hello!&lt;/b&gt;
B:Hello!
*/
</code></pre>