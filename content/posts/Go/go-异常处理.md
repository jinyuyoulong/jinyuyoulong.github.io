---
title: Go异常处理
date: 2019-02-18 15:48:37
tags:
categories: [Go]
---
<pre><code class="language-go line-numbers">type error interface {
    Error() string
}
</code></pre>

error的声明

创建一个error

<pre><code class="language-go line-numbers">if path == "" {
    return nil, errors.New("The parameter is invalid!")
}
</code></pre>

error的使用

<pre><code class="language-go line-numbers">func readFile(path string) ([]byte, error) {
    file, err := os.Open(path)
    if err != nil {
        return nil, err
    }
    defer file.Close()
    return ioutil.ReadAll(file)
}
</code></pre>

## 异常处理——panic

译为运行时恐慌

内建函数`panic`和`recover`是天生的一对。前者用于产生运行时恐慌，而后者用于“恢复”它。

不过要注意，`recover`函数必须要在`defer`语句中调用才有效。因为一旦有运行时恐慌发生，当前函数以及在调用栈上的所有代码都是失去对流程的控制权。只有`defer`语句携带的函数中的代码才可能在运行时恐慌迅速向调用栈上层蔓延时“拦截到”它。

<pre><code class="language-go line-numbers">defer func() {
    if p := recover(); p != nil {
        fmt.Printf("Fatal error: %s\n", p)
    }
}()
</code></pre>

`panic`函数。该函数可接受一个`interface{}`类型的值作为其参数。也就是说，我们可以在调用`panic`函数的时候可以传入任何类型的值。不过，我建议大家在这里只传入`error`类型的值。这样它表达的语义才是精确的。更重要的是，当我们调用`recover`函数来“恢复”由于调用`panic`函数而引发的运行时恐慌的时候，得到的值正是调用后者时传给它的那个参数。因此，有这样一个约定是很有必要的。

用法

<pre><code class="language-go line-numbers">package main
import (
    "errors"
    "fmt"
)
func innerFunc() {
    fmt.Println("Enter innerFunc")
    panic(errors.New("Occur a panic!"))
    fmt.Println("Quit innerFunc")
}
func outerFunc() {
    fmt.Println("Enter outerFunc")
    defer func() {
        if p := recover(); p != nil {
            fmt.Printf("Fatal error: %s\n", p)
        }
    }()
    innerFunc()
    fmt.Println("Quit outerFunc")
}
func main() {
    fmt.Println("Enter main")
    outerFunc()
    fmt.Println("Quit main")
}
</code></pre>

## go语句

`go`语句的执行会很快结束，并不会对当前流程的进行造成阻塞或明显的延迟。

在`go`语句被执行时，其携带的函数（也被称为`go`函数）以及要传给它的若干参数（如果有的话）会被封装成一个实体（即Goroutine），并被放入到相应的待运行队列中。Go语言的运行时系统会适时的从队列中取出待运行的Goroutine并执行相应的函数调用操作。注意，对传递给这里的函数的那些参数的求值会在`go`语句被执行时进行。这一点也是与`defer`语句类似的。

由于`go`函数的执行时间的不确定性，所以Go语言提供了很多方法来帮助我们协调它们的执行。其中最简单粗暴的方法就是调用`time.Sleep`函数。

<pre><code class="language-go line-numbers">package main
import (
    "fmt"
    "time"
)
func main() {
    go fmt.Println("Go!")
    time.Sleep(100 * time.Millisecond)
}
</code></pre>

另一个比较绅士的做法是在`main`函数的最后调用`runtime.Gosched`函数。

<pre><code class="language-go line-numbers">package main
import (
    "fmt"
    "runtime"
)
func main() {
    go fmt.Println("Go!")
    runtime.Gosched()
}
</code></pre>

`runtime.Gosched`函数的作用是让当前正在运行的Goroutine（这里是运行`main`函数的那个Goroutine）暂时“休息”一下，而让Go运行时系统转去运行其它的Goroutine（这里是与`go fmt.Println("Go!")`对应并会封装`fmt.Println("Go!")`的那个Goroutine）。如此一来，我们就更加精细地控制了对几个Goroutine的运行的调度。

<pre><code class="language-go line-numbers">package main
import (
    "fmt"
    "sync"
)
func main() {
    var wg sync.WaitGroup
    wg.Add(3)
    go func() {
        fmt.Println("Go!")
        wg.Done()
    }()
    go func() {
        fmt.Println("Go!")
        wg.Done()
    }()
    go func() {
        fmt.Println("Go!")
        wg.Done()
    }()
    wg.Wait()
}
</code></pre>

`sync.WaitGroup`类型有三个方法可用——`Add`、`Done`和`Wait`。`Add`会使其所属值的一个内置整数得到相应增加，`Done`会使那个整数减`1`，而`Wait`方法会使当前Goroutine（这里是运行`main`函数的那个Goroutine）阻塞直到那个整数为``。这下你应该明白上面这个示例所采用的方法了。我们在`main`函数中启用了三个Goroutine来封装三个`go`函数。每个匿名函数的最后都调用了`wg.Done`方法，并以此表达当前的`go`函数会立即执行结束的情况。当这三个`go`函数都调用过`wg.Done`函数之后，处于`main`函数最后的那条`wg.Wait()`语句的阻塞作用将会消失，`main`函数的执行将立即结束。

<pre><code class="language-go line-numbers">func main() {
    ch1 := make(chan int, 1)
    ch2 := make(chan int, 1)
    ch3 := make(chan int, 1)
    go func() {
        fmt.Println("1")
        ch1 &lt;- 1
    }()
    go func() {
        fmt.Println("2")
        ch2 &lt;- 2
    }()
    go func() {
        fmt.Println("3")
        ch3 &lt;- 3
    }()
    &lt;-ch3
}
/*
最终 print ：
1
2
3
*/
</code></pre>