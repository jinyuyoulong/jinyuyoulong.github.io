---
title: Go Crontab
author: fan
type: post
date: 2019-07-19T10:18:33+00:00
url: /go-crontab/
categories:
  - Go
  - 操作系统
tags:
  - Go

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

<pre><code class="language-go line-numbers">c := cron.New()
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
</code></pre>

### CRON表达格式

cron表达式表示一组时间，使用5个以空格分隔的字段。
  
| 字段名称 | 强制性？ | 允许值 | 允许特殊字符 |
  
| &#8212;&#8212;&#8212;&#8212;&#8211; | &#8212;&#8212;&#8211; | &#8212;&#8212;&#8212;&#8212;- | &#8212;&#8212;&#8212;&#8212; |
  
| 分钟 | 是的 | 0-59 | * /， &#8211; |
  
| 小时 | 是的 | 0-23 | * /， &#8211; |
  
| 一个月的某一天 | 是的 | 1-31 | * /， &#8211; ？ |
  
| 月 | 是的 | 1-12或JAN-DEC | * /， &#8211; |
  
| 星期几 | 是的 | 0-6或SUN-SAT | * /， &#8211; ？ |
  
月份和星期几字段值不区分大小写。“SUN”，“Sun”和“sun”同样被接受。
  
该格式的具体解释基于Cron维基百科页面：https://en.wikipedia.org/wiki/Cron

### 替代格式

**备用Cron表达式格式支持其他字段，如秒。您可以通过创建自定义Parser来实现，如下所示。**
  
cron.New（
      
cron.WithParser（
          
cron.NewParser（
              
cron.SecondOptional | cron.Minute | cron.Hour | cron.Dom | cron.Month | cron.Dow | cron.Descriptor）））
  
\*\*由于添加Seconds是对标准cron规范的最常见修改，cron提供了一个内置函数来执行此操作，这相当于您之前看到的自定义解析器，除了它的秒字段是必需的: \*\*
  
cron.New（cron.WithSeconds（））
  
这模仿Quartz，最流行的替代Cron计划格式：http://www.quartz-scheduler.org/documentation/2.4.0-SNAPSHOT/tutorials/tutorial-lesson-06.html

<pre><code class="language-sh line-numbers"> # ┌───────────── min (0 - 59)
 # │ ┌────────────── hour (0 - 23)
 # │ │ ┌─────────────── day of month (1 - 31)
 # │ │ │ ┌──────────────── month (1 - 12)
 # │ │ │ │ ┌───────────────── day of week (0 - 6) (0 to 6 are Sunday to
 # │ │ │ │ │                  Saturday, or use names; 7 is also Sunday)
 # │ │ │ │ │
 # │ │ │ │ │
 # * * * * *  command to execute
</code></pre>

## cron特定字符说明

特殊字符
  
星号（*）
  
星号表示cron表达式将匹配该字段的所有值; 例如，在第5个字段（月）中使用星号表示每个月。
  
斜线（/）
  
斜杠用于描述范围的增量。例如，第1场（分钟）中的3-59 / 15表示小时的第3分钟，之后每15分钟。形式“* \ / &#8230;”等同于“first-last / &#8230;”形式，即在该字段的最大可能范围内的增量。形式“N / &#8230;”被接受为“N-MAX / &#8230;”，即从N开始，使用增量直到该特定范围的结束。它没有环绕。
  
逗号（，）
  
逗号用于分隔列表的项目。例如，在第5个字段（星期几）中使用“MON，WED，FRI”将表示星期一，星期三和星期五。
  
连字符（ &#8211; ）
  
连字符用于定义范围。例如，9-17表示每天上午9点到下午5点之间的每小时。
  
问号（？）
  
可以使用问号而不是&#8217;*&#8217;来留下日期或星期几的空白。

#### 预定义的时间表

您可以使用几个预定义的计划之一来代替cron表达式。

| 进入                  | 说明           | 相当于           |
| ------------------- | ------------ | ------------- |
| @yearly（或@annually） | 每年一次，午夜，1月1日 | 0 0 1 1 *     |
| @monthly            | 每月运行一次，午夜，月初 | 0 0 1 \* \*   |
| @weekly             | 每周一次，午睡/周日午夜 | 0 0 \* \* 0   |
| @daily（或@midnight）  | 每天运行一次，午夜    | 0 0 \* \* *   |
| @hourly             | 每小时运行一次，小时开始 | 0 \* \* \* \* |

#### 间隔

您还可以安排作业以固定的时间间隔执行，从添加或运行cron开始。这可以通过格式化cron规范来支持，如下所示:
  
@every <duration>
  
其中“duration”是time.ParseDuration（http://golang.org/pkg/time/#ParseDuration）接受的字符串。
  
例如，“@ every 1h30m10s”表示在1小时30分10秒之后激活的计划，然后是之后的每个间隔。
  
注意: 间隔不会考虑作业运行时。例如，如果作业需要3分钟才能运行，并且计划每5分钟运行一次，则每次运行之间只有2分钟的空闲时间。

### cron举例说明

<pre><code class="language-go line-numbers">每隔1分钟执行一次:  */1 * * * ?
每天23点执行一次:  0 23 * * ?
每天凌晨1点执行一次:  0 1 * * ?
每月1号凌晨1点执行一次:  0 1 1 * ?
在26分、29分、33分执行一次:  26,29,33 * * * ?
每天的0点、13点、18点、21点都执行一次:  0 0,13,18,21 * * ?
</code></pre>

#### 时区

默认情况下，所有解释和计划都在计算机的本地时区（time.Local）中完成。您可以在构造中指定不同的时区:

<pre><code class="language-go line-numbers">cron.New(
    cron.WithLocation(time.UTC))
</code></pre>

单个cron调度还可以通过在cron规范的开头提供`CRON_TZ=Asia/Tokyo`.覆盖它们将被解释的时区。
  
例如:

<pre><code class="language-go line-numbers"># Runs at 6am in time.Local
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
</code></pre>

传统兼容性还支持前缀“TZ =(TIME ZONE)”。
  
请注意，在夏令时跨越式过渡期间安排的作业将无法运行！
  
作业包装机/链条
  
Cron运行器可以配置一系列作业包装器，以便为所有提交的作业添加横切功能。例如，它们可用于实现以下效果:

  * 从作业中恢复任何恐慌（默认激活）
  * 如果先前的运行尚未完成，则延迟作业的执行
  * 如果之前的运行尚未完成，则跳过作业的执行
  * 记录每个作业的调用
  
    使用`cron.WithChain`选项为添加到cron的所有作业安装包装器:

<pre><code class="language-go line-numbers">cron.New(cron.WithChain(
    cron.SkipIfStillRunning(logger),
))
</code></pre>

通过显式包装它们来为各个作业安装包装器:

<pre><code class="language-go line-numbers">job = cron.NewChain(
    cron.SkipIfStillRunning(logger),
).Then(job)
</code></pre>

线程安全
  
由于Cron服务与调用代码同时运行，因此必须采取一些措施以确保正确同步。
  
只要调用者确保调用在它们之间进行排序之前有明确的发生，所有cron方法都被设计为正确同步。
  
记录
  
Cron定义了一个Logger接口，它是github.com/go-logr/logr中定义的接口的一个子集。它有两个日志记录级别（信息和错误），参数是键/值对。这使得cron日志记录可以插入结构化日志记录系统。提供了一个适配器[Verbose] PrintfLogger来包装标准库* log.Logger。
  
为了进一步了解Cron操作，可以激活详细日志记录，这将记录作业运行，调度决策以及添加或删除的作业。使用一次性记录器激活它，如下所示:

<pre><code class="language-go line-numbers">cron.New(
    cron.WithLogger(
        cron.VerbosePrintfLogger(log.New(os.Stdout, "cron: ", log.LstdFlags))))
</code></pre>

履行
  
Cron条目存储在一个数组中，按其下一个激活时间排序。Cron睡着，直到下一份工作开始运行。
  
醒来后:

  * 它运行在该秒钟上处于活动状态的每个条目
  * 它计算运行的作业的下一个运行时间
  * 它按下一个激活时间重新排序条目数组。
  * 它会一直睡到最快的工作。