---
title: "Go Crontab v3"
date: 2019-07-19T16:51:27+08:00
categories: [ Go]
---

[TOC]

---

## 关于cron更新

### Cron V3已经发布！

要下载特定的标记版本，请运行: 

`go get github.com/robfig/cron/v3@v3.0.0`
将其导入您的程序中: 

`import "github.com/robfig/cron/v3"`
由于Go Modules的使用，它需要Go 1.11或更高版本。

请参阅此处的文档：http://godoc.org/github.com/robfig/cron

本文档的其余部分介绍了v3的进展以及希望从早期版本升级的用户的重大更改列表。

升级到v3(2019年6月)
cron v3是对库的重大升级，可以解决所有未解决的错误，功能请求和粗糙边缘。它基于master的合并，其中包含对多年来发现的问题的各种修复，以及v2分支，其中包含一些向后兼容的功能，例如删除cron作业的功能。此外，v3增加了对Go Modules的支持，清除了时区支持等粗糙边缘，并修复了许多错误。

### 新功能: 

**支持Go模块。调用者现在必须导入此库 github.com/robfig/cron/v3，而不是gopkg.in/...**

修正了错误: 

0f01e6b 解析器: 修复Dow和Dom的组合(＃70)
dbf3220 在向前滚动时钟时调整时间以处理不存在的午夜(＃157)
eeecf15 spec_test.go：确保在0增量处返回错误(＃144)
70971dc cron.Entries(): 更新快照请求以包含回复通道(＃97)
1cba5e6 cron：修复: 删除作业导致下一个预定作业运行得太晚(＃206)
标准cron规范默认解析(第一个字段是“分钟”)，可以轻松选择进入秒字段(石英兼容)。虽然，请注意不支持年份字段(Quartz中的可选)。

通过符合https://github.com/go-logr/logr项目的接口进行可扩展的键/值记录。

新的Chain＆JobWrapper类型允许您安装“拦截器”以添加如下所示的横切行为: 

从工作中恢复任何恐慌
如果先前的运行尚未完成，则延迟作业的执行
如果先前的运行尚未完成，则跳过作业的执行
记录每个作业的调用
作业完成时的通知
它向后与v1和v2不兼容。这些更新是必需的: 

**v1分支在cron规范的开头接受了一个可选的秒字段。这是非标准的，并导致了很多混乱。新的默认解析器符合Cron维基百科页面所描述的标准。**

更新: 要保留旧行为，请使用自定义解析器构建您的Cron：
```go
// Seconds field, required
cron.New(cron.WithSeconds())

// Seconds field, optional
cron.New(
    cron.WithParser(
        cron.SecondOptional | cron.Minute | cron.Hour | cron.Dom | cron.Month | cron.Dow | cron.Descriptor))
```
最常见的改造是添加秒，v3为我们提供了内置的方法实现：

```go
	c := cron.New(cron.WithSeconds())
	// 此处space 多了一个 seconds 的解析符
	space := "*/1 * * * * *"
	c.AddFunc(space, func() {
		fmt.Println("Every seconds action")
	})

	c.Start()
	select {}
```



Cron类型现在接受构造上的功能选项而不是先前的特殊行为修改机制(设置字段，调用setter)。

更新: 必须更新设置Cron.ErrorLogger或调用Cron.SetLocation的代码以在构造时提供这些值。

**CRON_TZ现在是指定单个计划的时区的推荐方法，该计划由规范批准。遗留的“TZ =”前缀将继续得到支持，因为它是明确且易于执行的。**

更新: 无需更新。

**默认情况下，cron将不再恢复其运行的作业中的恐慌。**恢复可能会令人惊讶(参见问题＃192)，似乎与图书馆的典型行为不一致。相关地，该cron.WithPanicLogger选项已被删除以适应更通用的JobWrapper类型。

更新: 选择进行恐慌恢复并配置恐慌记录器: 

cron.New(cron.WithChain(
    cron.Recover(logger),  // or use cron.DefaultLogger
))
在添加对https://github.com/go-logr/logr的支持时，cron.WithVerboseLogger已删除，因为它与级别日志记录重复。

更新: 调用者应使用WithLogger并指定不丢弃Info日志的记录器。为方便起见，提供了一个包装*log.Logger：

cron.New(
    cron.WithLogger(cron.VerbosePrintfLogger(logger)))
### 背景 - Cron spec格式
**常用的有两种cron规范格式: **

**“标准”cron格式，在Cron维基百科页面上描述，由cron Linux系统实用程序使用。** 格式为5位，没有秒级

**Quartz Scheduler使用的cron格式，通常用于Java软件中的预定作业**

`CronExpression cexp = new CronExpression("0/5 * * * * ?");` Quartz格式为6位，和v1版本一样。

该软件包的原始版本包含一个可选的“秒”字段，这使得它与这两种格式都不兼容。现在，“标准”格式是接受的默认格式，Quartz格式是选择加入的。