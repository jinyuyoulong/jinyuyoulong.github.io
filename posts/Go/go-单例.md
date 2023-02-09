---
title: Go 单例
date: 2019-05-27
categories: [Go]
---
为什么使用单例？

由于Go的多协程机制，当只是单核的时候，变量还不会出现问题，但是当设置成多核之后，就会涉及到变量的作用域问题，只用普通方式常见的变量在其他线程上会得到错误的方法

---
单例的作用不用我多说，大家都知道，那么在go中如何构造单例呢，下面是我的总结。

一、 sync.Once用法

在Go中有一个简洁的方法就是使用sync.Once，它可以在多协程中起到控制作用。实现起来也非常简单。

<pre><code class="language-go line-numbers">var (
    once     sync.Once
    instance *SingleTon
)
func GetInstance(str string) *SingleTon {
    once.Do(func() {
        instance = &SingleTon{Attr: str}
    })
    return instance
}
</code></pre>

二、使用加锁机制

在Go语言中有个基础对象sync.Mutex，可以实现协程之间的同步逻辑。

<pre><code class="language-go line-numbers">var mu sync.Mutex
func GetInstance() *SingleTon {
  mu.Lock()
  defer mu.Unock()
    if Instance == nil {
        instance = &SingleTon{}
    }
    return instance
}
</code></pre>

三、简单粗暴模式.

这种方式实现起来特别简单，直接判断一个实力是不是为nil， 如果是，则新生成；否则返回已有的。但它和多数语言一样，只适合用在单线程。这个就很鸡肋，几乎没有什么应用场景，倒是bug经常出在这里。

<pre><code class="language-go line-numbers">type SingleTon struct {
}
var instance *SingleTon
func GetInstance() *SingleTon {
    if Instance == nil {
        instance = &SingleTon{}
    }
    return instance
}
</code></pre>

测试代码如下，从运行结果来看，都是一致的。

<pre><code class="language-go line-numbers">func main() {
    for i := 0; i &lt; 10; i++ {
        go func() {
            s := GetInstance("test:" + strconv.Itoa(i))
            s.TestFunc()
        }()
    }
    time.Sleep(1e5)
}
</code></pre>