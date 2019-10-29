---
title: Go gRPC研究总结
date: 2019-04-11
categories:
  - Go
---

### 什么是RPC

RPC（Remote Procedure Call）—远程过程调用，它是一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的协议。RPC协议假定某些传输协议的存在，如TCP或UDP，为通信程序之间携带信息数据。在OSI网络通信模型中，RPC跨越了传输层和应用层。RPC使得开发包括网络分布式多程序在内的应用程序更加容易。——百度百科

支持环境配置(Mac)

安装protobuf 这是 Google 开源的一套成熟的结构数据序列化机制[protocol buffer](https://juejin.im/post/5b852d476fb9a019e4505873) 

```protobuf
brew info protobuf
brew install protobuf
```

检验protobuf安装结果

```shell
protoc --version
libprotoc 3.5.1
```

安装第三方包

```go
go mod download github.com/golang/protobuf/proto
go mod download github.com/golang/protobuf/protoc-gen-go
go mod download google.golang.org/grpc
go install github.com/golang/protobuf/protoc-gen-go //编译 protoc-gen-go 可执行文件
```

创建 protobuf 文件

```shell
vi add.proto
add some date
```

生成 gRPC 代码

```shell
protoc -I ./protos ./protos/helloworld.proto --go_out=plugins=grpc:helloworld
或
protoc -I . add.proto --go_out=plugins=grpc:.
```

这生成了 `helloworld.pb.go` ，包含了我们生成的客户端和服务端类，此外还有用于填充、序列化、提取 `HelloRequest` 和 `HelloResponse` 消息类型的类。



在server.go 实现AddServiceServer 的接口方法

```go
type HelloServer struct {
}

func (h HelloServer) SayHello(c context.Context, in *pb.HelloRequest) (*pb.HelloReply, error) {
	return &pb.HelloReply{Message: "hello " + in.Name}, nil
}	
```



实现server & client

打开两个终端，分别启动 serve & client

浏览器访问输出返回结果。