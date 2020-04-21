---
title: Go-流程控制
<<<<<<< HEAD:posts/2019-02-19-go-流程控制.md
author: fan
type: post
date: 2019-02-19T05:08:57+00:00
url: /go-流程控制/
categories:
  - Go
=======
date: 2019-02-18 11:38:16
categories: [Go]
---

[TOC]
>>>>>>> 9b93207d813e2b213031f967612e37c68194cf37:post/Go-流程控制.md

---
if

<pre><code class="language-go line-numbers">if 100 &gt; number {
    number += 3
} else if 100 &lt; number {
    number -= 2
} else {
    fmt.Println("OK!")
}
</code></pre>

<pre><code class="language-go line-numbers">//变量赋值
if number := 4; 100 &gt; number {
    number += 3
}
</code></pre>

<pre><code class="language-go line-numbers">// 标识符的重声明和标识符的遮蔽
var number int
if number := 4; 100 &gt; number {
    number += 3
}
</code></pre>

**标识符的重声明和标识符的遮蔽**
  
上述代码被执行完毕之后，第二次声明的`number`变量的值会是`7`，而第一次声明的`number`变量的值仍会是``。
  
switch

<pre><code class="language-go line-numbers">names := []string{"Golang", "Java", "Rust", "C"}
switch name := names[0]; name {
case "Golang":
    fmt.Println("A programming language from Google.")
case "Rust":
    fmt.Println("A programming language from Mozilla.")
default:
    fmt.Println("Unknown!")
}
</code></pre>

<pre><code class="language-go line-numbers">v := 11
switch i := interface{}(v).(type) {
case int, int8, int16, int32, int64:
    fmt.Printf("A signed integer: %d. The type is %T. \n", i, i)
case uint, uint8, uint16, uint32, uint64:
    fmt.Printf("A unsigned integer: %d. The type is %T. \n", i, i)
default:
    fmt.Println("Unknown!")
}
</code></pre>

## for语句

<pre><code class="language-go line-numbers">for i := 0; i &lt; 10; i++ {
    fmt.Print(i, " ")
}
</code></pre>

<pre><code class="language-go line-numbers">for i, v := range "Go语言" {
    fmt.Printf("%d: %c\n", i, v)
}
/* print
0: G
1: o
2: 语
5: 言
*/
// 注意，一个中文字符在经过UTF-8编码之后会表现为三个字节。
/*
range表达式的结果值的类型应该是能够被迭代的，包括：
字符串类型、
数组类型、
数组的指针类型、
切片类型、
字典类型
通道类型
for语句每次会迭代出两个值。
第一个值代表第二个值在字符串中的索引，
第二个值则代表该字符串中的某一个字符。
*/
</code></pre>

最后，我们来说一下`break`语句和`continue`语句。它们都可以被放置在`for`语句的代码块中。break被执行时会使其所属的`for`语句的执行立即结束，continue被执行时会使当次迭代被中止（当次迭代的后续语句会被忽略）而直接进入到下一次迭代。

## select语句

`select`语句属于条件分支流程控制方法，不过它只能用于通道。它可以包含若干条`case`语句，并根据条件选择其中的一个执行。进一步说，`select`语句中的`case`关键字只能后跟用于通道的发送操作的表达式以及接收操作的表达式或语句。

<pre><code class="language-go line-numbers">ch1 := make(chan int, 1)
ch2 := make(chan int, 1)
// 省略若干条语句
select {
case e1 := &lt;-ch1:
    fmt.Printf("1th case is selected. e1=%v.\n", e1)
case e2 := &lt;-ch2:
    fmt.Printf("2th case is selected. e2=%v.\n", e2)
default:
    fmt.Println("No data!")
}
</code></pre>

如果该`select`语句被执行时通道`ch1`和`ch2`中都没有任何数据，那么肯定只有`default case`会被执行。但是，只要有一个通道在当时有数据就不会轮到`default case`执行了。显然，对于包含通道接收操作的`case`来讲，其执行条件就是通道中存在数据（或者说通道未空）。如果在当时有数据的通道多于一个，那么Go语言会通过一种伪随机的算法来决定哪一个`case`将被执行。
  
我们一直在说`case`执行条件的满足与否取决于其操作的通道在当时的状态。这里特别强调一点，即：未被初始化的通道会使操作它的`case`永远满足不了执行条件。对于针对它的发送操作和接收操作来说都是如此。

<pre><code class="language-go line-numbers">ch4 := make(chan int, 1)
for i := 0; i &lt; 4; i++ {
    select {
    case e, ok := &lt;-ch4:
        if !ok {
            fmt.Println("End.")
            return
        }
        fmt.Println(e)
        close(ch4)
    default:
        fmt.Println("No Data!")
        ch4 &lt;- 1
    }
}
</code></pre>

## defer语句 [dɪˈfɚ] 推迟

`defer`语句仅能被放置在函数或方法中。它由关键字`defer`和一个调用表达式组成。注意，这里的调用表达式所表示的既不能是对Go语言内建函数的调用也不能是对Go语言标准库代码包`unsafe`中的那些函数的调用。

<pre><code class="language-go line-numbers">func readFile(path string) ([]byte, error) {
    file, err := os.Open(path)
    if err != nil {
        return nil, err
    }
    defer file.Close()
    return ioutil.ReadAll(file)
}
</code></pre>

注意，当这条`defer`语句被执行的时候，其中的这条表达式语句并不会被立即执行。它的确切的执行时机是在其所属的函数（这里是`readFile`）的执行即将结束的那个时刻。也就是说，在`readFile`函数真正结束执行的前一刻，`file.Close()`才会被执行。
  
注意，当一个函数中存在多个`defer`语句时，它们携带的表达式语句的执行顺序一定是它们的出现顺序的倒序。
  
最后，对于`defer`语句，我还有两个特别提示：

  1. `defer`携带的表达式语句代表的是对某个函数或方法的调用。这个调用可能会有参数传入，比如：`fmt.Print(i + 1)`。如果代表传入参数的是一个表达式，那么在`defer`语句被执行的时候该表达式就会被求值了。注意，这与被携带的表达式语句的执行时机是不同的。
  2. 如果defer携带的表达式语句代表的是对匿名函数的调用，那么我们就一定要非常警惕。正确的用法是：把要使用的外部变量作为参数传入到匿名函数中。

<pre><code class="language-go line-numbers">func deferIt4() {
    for i := 1; i &lt; 5; i++ {
        defer func(n int) {
            fmt.Print(n)
        }(i)
    }
}
</code></pre>