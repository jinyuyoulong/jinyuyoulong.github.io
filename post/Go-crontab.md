---
title: "Go Crontab"
date: 2019-07-19T16:51:27+08:00
categories:
  "Go-crontab"
---

[TOC]

# 计划任务

from Godoc

包cron实现了cron规范解析器和作业运行器。

安装
要下载特定的标记版本，请运行: 

`go get github.com/robfig/cron/v3@v3.0.0`
将其导入您的程序中: 

`import “github.com/robfig/cron/v3”`
由于Go Modules的使用，它需要Go 1.11或更高版本。

用法
呼叫者可以在给定的时间表上注册要调用的Func。Cron将在他们自己的goroutines中运行它们。

```go
c := cron.New()
c.AddFunc("30 * * * *", func() { fmt.Println("Every hour on the half hour") })
c.AddFunc("30 3-6,20-23 * * *", func() { fmt.Println(".. in the range 3-6am, 8-11pm") })
c.AddFunc("CRON_TZ=Asia/Tokyo 30 04 * * * *", func() { fmt.Println("Runs at 04:30 Tokyo time every day") })
c.AddFunc("@hourly",      func() { fmt.Println("Every hour, starting an hour from now") })
c.AddFunc("@every 1h30m", func() { fmt.Println("Every hour thirty, starting an hour thirty from now") })
c.Start()
..
// Funcs are invoked in their own goroutine, asynchronously.
...
// Funcs may also be added to a running Cron
c.AddFunc("@daily", func() { fmt.Println("Every day") })
..
// Inspect the cron job entries' next and previous run times.
inspect(c.Entries())
..
c.Stop()  // Stop the scheduler (does not stop any jobs already running).
```

### CRON表达格式
cron表达式表示一组时间，使用5个以空格分隔的字段。

| 字段名称       | 强制性？ | 允许值        | 允许特殊字符 |
| -------------- | -------- | ------------- | ------------ |
| 分钟           | 是的     | 0-59          | * /， -      |
| 小时           | 是的     | 0-23          | * /， -      |
| 一个月的某一天 | 是的     | 1-31          | * /， - ？   |
| 月             | 是的     | 1-12或JAN-DEC | * /， -      |
| 星期几         | 是的     | 0-6或SUN-SAT  | * /， - ？   |
月份和星期几字段值不区分大小写。“SUN”，“Sun”和“sun”同样被接受。

该格式的具体解释基于Cron维基百科页面：https://en.wikipedia.org/wiki/Cron

### 替代格式

**备用Cron表达式格式支持其他字段，如秒。您可以通过创建自定义Parser来实现，如下所示。**

cron.New（
	cron.WithParser（
		cron.NewParser（
			cron.SecondOptional | cron.Minute | cron.Hour | cron.Dom | cron.Month | cron.Dow | cron.Descriptor）））
**由于添加Seconds是对标准cron规范的最常见修改，cron提供了一个内置函数来执行此操作，这相当于您之前看到的自定义解析器，除了它的秒字段是必需的: **

cron.New（cron.WithSeconds（））
这模仿Quartz，最流行的替代Cron计划格式：http://www.quartz-scheduler.org/documentation/2.4.0-SNAPSHOT/tutorials/tutorial-lesson-06.html



```sh
 # ┌───────────── min (0 - 59)
 # │ ┌────────────── hour (0 - 23)
 # │ │ ┌─────────────── day of month (1 - 31)
 # │ │ │ ┌──────────────── month (1 - 12)
 # │ │ │ │ ┌───────────────── day of week (0 - 6) (0 to 6 are Sunday to
 # │ │ │ │ │                  Saturday, or use names; 7 is also Sunday)
 # │ │ │ │ │
 # │ │ │ │ │
 # * * * * *  command to execute
```
## cron特定字符说明
特殊字符
星号（*）

星号表示cron表达式将匹配该字段的所有值; 例如，在第5个字段（月）中使用星号表示每个月。

斜线（/）

斜杠用于描述范围的增量。例如，第1场（分钟）中的3-59 / 15表示小时的第3分钟，之后每15分钟。形式“* \ / ...”等同于“first-last / ...”形式，即在该字段的最大可能范围内的增量。形式“N / ...”被接受为“N-MAX / ...”，即从N开始，使用增量直到该特定范围的结束。它没有环绕。

逗号（，）

逗号用于分隔列表的项目。例如，在第5个字段（星期几）中使用“MON，WED，FRI”将表示星期一，星期三和星期五。

连字符（ - ）

连字符用于定义范围。例如，9-17表示每天上午9点到下午5点之间的每小时。

问号（？）

可以使用问号而不是'*'来留下日期或星期几的空白。

#### 预定义的时间表
您可以使用几个预定义的计划之一来代替cron表达式。


进入| 说明| 相当于
----- | ----------- -------------
@yearly（或@annually）| 每年一次，午夜，1月1日| 0 0 1 1 *
@monthly | 每月运行一次，午夜，月初| 0 0 1 * *
@weekly | 每周一次，午睡/周日午夜| 0 0 * * 0
@daily（或@midnight）| 每天运行一次，午夜| 0 0 * * *
@hourly | 每小时运行一次，小时开始| 0 * * * *
#### 间隔
您还可以安排作业以固定的时间间隔执行，从添加或运行cron开始。这可以通过格式化cron规范来支持，如下所示: 

@every <duration>
其中“duration”是time.ParseDuration（http://golang.org/pkg/time/#ParseDuration）接受的字符串。

例如，“@ every 1h30m10s”表示在1小时30分10秒之后激活的计划，然后是之后的每个间隔。

注意: 间隔不会考虑作业运行时。例如，如果作业需要3分钟才能运行，并且计划每5分钟运行一次，则每次运行之间只有2分钟的空闲时间。

### cron举例说明
```go
每隔1分钟执行一次:  */1 * * * ?
每天23点执行一次:  0 23 * * ?
每天凌晨1点执行一次:  0 1 * * ?
每月1号凌晨1点执行一次:  0 1 1 * ?
在26分、29分、33分执行一次:  26,29,33 * * * ?
每天的0点、13点、18点、21点都执行一次:  0 0,13,18,21 * * ?
```
#### 时区
默认情况下，所有解释和计划都在计算机的本地时区（time.Local）中完成。您可以在构造中指定不同的时区: 

```go
cron.New(
    cron.WithLocation(time.UTC))
```

单个cron调度还可以通过在cron规范的开头提供`CRON_TZ=Asia/Tokyo`.覆盖它们将被解释的时区。

例如:

```go
# Runs at 6am in time.Local
cron.New().AddFunc("0 6 * * ?", ...)

# Runs at 6am in America/New_York
nyc, _ := time.LoadLocation("America/New_York")
c := cron.New(cron.WithLocation(nyc))
c.AddFunc("0 6 * * ?", ...)

# Runs at 6am in Asia/Tokyo
cron.New().AddFunc("CRON_TZ=Asia/Tokyo 0 6 * * ?", ...)

# Runs at 6am in Asia/Tokyo
c := cron.New(cron.WithLocation(nyc))
c.SetLocation("America/New_York")
c.AddFunc("CRON_TZ=Asia/Tokyo 0 6 * * ?", ...)
```

传统兼容性还支持前缀“TZ =(TIME ZONE)”。

请注意，在夏令时跨越式过渡期间安排的作业将无法运行！

作业包装机/链条

Cron运行器可以配置一系列作业包装器，以便为所有提交的作业添加横切功能。例如，它们可用于实现以下效果: 

- 从作业中恢复任何恐慌（默认激活）
- 如果先前的运行尚未完成，则延迟作业的执行
- 如果之前的运行尚未完成，则跳过作业的执行
- 记录每个作业的调用
使用`cron.WithChain`选项为添加到cron的所有作业安装包装器: 

```go
cron.New(cron.WithChain(
	cron.SkipIfStillRunning(logger),
))
```

通过显式包装它们来为各个作业安装包装器: 

```go
job = cron.NewChain(
	cron.SkipIfStillRunning(logger),
).Then(job)
```

线程安全 
由于Cron服务与调用代码同时运行，因此必须采取一些措施以确保正确同步。

只要调用者确保调用在它们之间进行排序之前有明确的发生，所有cron方法都被设计为正确同步。

记录
Cron定义了一个Logger接口，它是github.com/go-logr/logr中定义的接口的一个子集。它有两个日志记录级别（信息和错误），参数是键/值对。这使得cron日志记录可以插入结构化日志记录系统。提供了一个适配器[Verbose] PrintfLogger来包装标准库* log.Logger。

为了进一步了解Cron操作，可以激活详细日志记录，这将记录作业运行，调度决策以及添加或删除的作业。使用一次性记录器激活它，如下所示: 

```go
cron.New(
	cron.WithLogger(
		cron.VerbosePrintfLogger(log.New(os.Stdout, "cron: ", log.LstdFlags))))
```

履行
Cron条目存储在一个数组中，按其下一个激活时间排序。Cron睡着，直到下一份工作开始运行。

醒来后: 

- 它运行在该秒钟上处于活动状态的每个条目
- 它计算运行的作业的下一个运行时间
- 它按下一个激活时间重新排序条目数组。
- 它会一直睡到最快的工作。

---

## 关于cron更新

### Cron V3已经发布！

要下载特定的标记版本，请运行: 

go get github.com/robfig/cron/v3@v3.0.0
将其导入您的程序中: 

import "github.com/robfig/cron/v3"
由于Go Modules的使用，它需要Go 1.11或更高版本。

请参阅此处的文档：http： //godoc.org/github.com/robfig/cron

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

// Seconds field, required
cron.New(cron.WithSeconds())

// Seconds field, optional
cron.New(
    cron.WithParser(
        cron.SecondOptional | cron.Minute | cron.Hour | cron.Dom | cron.Month | cron.Dow | cron.Descriptor))

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

