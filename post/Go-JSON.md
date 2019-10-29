---
title: Go JSON
data: 2019-03-05
categories: [Go]
---



标准库

```
encoding/json、encoding/xml、encoding/asn1
```

Model

```go
type Movie struct {
    Title  string
    Year   int  `json:"released"`
    Color  bool `json:"color,omitempty"`
    Actors []string
}
// 赋值
var movies = []Movie{
    {Title: "Casablanca", Year: 1942, Color: false,
        Actors: []string{"Humphrey Bogart", "Ingrid Bergman"}},
    {Title: "Cool Hand Luke", Year: 1967, Color: true,
        Actors: []string{"Paul Newman"}},
    {Title: "Bullitt", Year: 1968, Color: true,
        Actors: []string{"Steve McQueen", "Jacqueline Bisset"}},
}
```

在编码时，默认使用Go语言结构体的成员名字作为JSON的对象（通过reflect反射技术，我们将在12.6节讨论）。只有导出的结构体成员才会被编码，这也就是我们为什么选择用大写字母开头的成员名称。

即使对应的JSON对象名是小写字母，每个结构体的成员名也是**声明为大写字母开头的**。因为有些JSON成员名字和Go结构体成员名字并不相同，因此需要Go语言结构体成员**Tag来指定对应的JSON名字**。同样，在解码的时候也需要做同样的处理，

