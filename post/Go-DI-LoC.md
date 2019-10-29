---
title: Go DI LoC研究
date: 2019-05-24
categories: [Go]
---

依赖注入，控制反转

目的：实现模块与项目的解耦



实现流程

首先模块有指针，其次DI拿到指针，再次DI将指针赋给调用者

共调研了三个框架：iris内置的di&mvc，uber-dig，google/wire

最终决定使用 wire

google DI 框架 wire
它通过使用代码生成构建容器来避免运行时反射。

用法：
```
// file main.go

package main
import "bytes"

type Logger struct{}

func (logger *Logger) Log(message string) {
	println(message)
}

type HttpClient struct {
	logger *Logger
}

func (client *HttpClient) Get(url string) string {
	client.logger.Log("Getting " + url)
	return "my response from " + url
}

func NewHttpClient(logger *Logger) *HttpClient {
	return &HttpClient{logger}
}

type ConcatService struct {
	logger *Logger
	client *HttpClient
}

func NewConcatService(logger *Logger, client *HttpClient) *ConcatService {
	return &ConcatService{logger, client}
}
func (service *ConcatService) GetAll(urls ...string) string {
	service.logger.Log("Runing GetAll")
	var result bytes.Buffer
	for _, url := range urls {
		result.WriteString(service.client.Get(url))
	}
	return result.String()
}

func main() {
	service := CreateConcatService()
	result := service.GetAll(
		"http://example.com",
		"https://drewolson.org",
	)
	println(result)
}

```
```
// file container.go

package main

import (
	"github.com/google/wire"
)

// CreateConcatService 设置 service 的依赖
// wire 生成 wire_gen.go 的 模板文件
func CreateConcatService() *ConcatService {
	panic(wire.Build(
		wire.NewSet(wire.Struct(new(Logger))), // struct 使用 wire.Struct 创建
		NewHttpClient,
		NewConcatService,
	))
}
// v0.2.2
func createxx()*ConcatService{
	panic(wire.Build(
		Logger{},
		NewHttpClient,
		NewConcatService,
	))
}
```

    $ go get github.com/google/wire/cmd/wire
    $ wire

执行 wire 解析 container.go ——> wire_gen.go
解析完毕后删除 container.go 文件, 使用 wire_gen.go 中的方法就行

wire当前版本v0.2.2 不支持 Struct,但是后期会废除`Logger{}`这种形式,官方推荐Struct。

所以结构体的初始化，尽量使用function，`NewStructName`，以避免后期的兼容性