---
title: Go HTML template
date: 2019-03-05
categories: [Go]
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

### 语法

```go
//取值
<p>{{.ArticleContent}}<span>{{.ArticleId}}</span></p>
// if 语句
{{if .condition}}
{{end}}

{{if .condition1}}
{{else if .contition2}}
{{end}}

// go 方法调用
{{funcname .arg1 .arg2}}
func add(left int, right int) int
{{add 1 2}}

// 逻辑判断
not 非
{{if not .condition}}
{{end}}

and 与
{{if and .condition1 .condition2}}
{{end}}

or 或
{{if or .condition1 .condition2}}
{{end}}

eq 等于
{{if eq .var1 .var2}}
{{end}}

ne 不等于
{{if ne .var1 .var2}}
{{end}}

lt 小于 (less than)
{{if lt .var1 .var2}}
{{end}}

le 小于等于
{{if le .var1 .var2}}
{{end}}

gt 大于
{{if gt .var1 .var2}}
{{end}}

ge 大于等于
{{if ge .var1 .var2}}
{{end}}

循环
{{range $i, $v := .slice}}
{{end}}

{{range .slice}}
{{.field}}
{{end}}

模板嵌套
{{template "navbar"}}// 使用
{{define "navbar"}}// 定义
{{end}}
{{template "navbar" .}}// 获取父模板的变量
```

参考https://www.kancloud.cn/cserli/golang/531904