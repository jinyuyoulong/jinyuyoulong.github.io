---
title: Go HTML template
date: 2019-03-05
categories:
  - Go
---

```go
文档
go doc text/template
$ go doc html/template
```

### 应用

```go

func main() {
    // 定义模板显示格式
	const templ = `<p>A: {{.A}}</p><p>B: {{.B}}</p>`
    // 模板配置函数
	t := template.Must(template.New("escape").Parse(templ))
	var data struct {
		A string        // untrusted plain text
		B template.HTML // trusted HTML
	}
    // A是一个普通字符串，B是一个信任的template.HTML字符串类型。
	data.A = "<b>Hello!</b>"
	data.B = "<b>Hello!</b>"
    // 使用定义好的 模板 输出到 控制台
	if err := t.Execute(os.Stdout, data); err != nil {
		log.Fatal(err)
	}
}

/*
autoescape.html 结果

A:<b>Hello!</b>
B:Hello!

*/
```

