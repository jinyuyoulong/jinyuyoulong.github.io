---
title: Go的函数 结构体
date: 2019-02-17 21:15:19
tags:
categories: [Go]
---

```go
func(input1 string ,input2 string) string
type MyFunc func(input1 string ,input2 string) string// 函数声明
```
函数实现
```go
func myFunc(part1 string, part2 string) (result string) {
    result = part1 + part2
    return
}
//如果结果声明是带名称的，那么它就相当于一个已被声明但未被显式赋值的变量。
//我们可以为它赋值且在return语句中省略掉需要返回的结果值。
```

或

```go
func myFunc(part1 string, part2 string) string {
    return part1 + part2
}  
```

```go
var splice func(string, string) string // 等价于 var splice MyFunc
//只要一个函数的参数声明列表和结果声明列表中的数据类型的顺序和名称与某一个函数类型完全一致，前者就是后者的一个实现。
```

```go
var result = func(part1 string, part2 string) string {
    return part1 + part2
}("1", "2")
```

结构体

```go
type Person struct {
    Name   string
    Gender string
    Age    uint8
}
Person{Name: "Robert", Gender: "Male", Age: 33} //赋值
Person{"Robert", "Male", 33}  //赋值顺序相同时，可以省略字段名
```

```go
//匿名结构体,不可能有方法
p := struct {
    Name   string
    Gender string
    Age    uint8
}{"Robert", "Male", 33}
```

```go
// 结构体方法
func (person *Person) Grow() {
    person.Age++
} 
p := Person{"Robert", "Male", 33}
p.Grow()   
```

与对象不同的是，结构体之间没有继承关系。

---

接口

```go
type Animal interface {
    Grow()
	Move(new string) (old string)
}
```

```go
p := Person{"Robert", "Male", 33, "Beijing"}
v := interface{}(&p)//空接口类型转换
h, ok := v.(Animal)//类型断言,判断结构体是否实现了 Animal 接口
```

如果一个数据类型所拥有的方法集合中包含了某一个接口类型中的所有方法声明的实现，那么就可以说这个数据类型实现了那个接口类型。

