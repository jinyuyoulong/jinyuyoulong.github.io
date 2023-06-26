---
title: Go DI LoC 依赖注入研究
author: fan
type: post
date: 2019-05-29T03:18:11+00:00
url: /go-di-loc-依赖注入研究/
primer_layout:
  - one-column-wide
categories:
  - Go
  - 其他技术
  - 设计
tags:
  - Go

---
依赖注入，控制反转 设计模式
  
目的：实现模块与项目的解耦
  
实现流程
  
首先模块有指针，其次DI拿到指针，再次DI将指针赋给调用者
  
共调研了三个框架：iris内置的di&mvc，uber-dig，google/wire
  
最终决定使用 wire
  
google DI 框架 wire
  
它通过使用代码生成构建容器来避免运行时反射。
  
用法：

<pre><code class="line-numbers">// file main.go
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
</code></pre>

<pre><code class="line-numbers">// file container.go
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
</code></pre>

    $ go get github.com/google/wire/cmd/wire
    $ wire
    

执行 wire 解析 container.go ——> wire_gen.go
  
解析完毕后删除 container.go 文件, 使用 wire_gen.go 中的方法就行