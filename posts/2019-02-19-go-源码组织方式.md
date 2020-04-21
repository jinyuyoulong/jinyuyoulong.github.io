---
title: Go-源码组织方式
author: fan
type: post
date: 2019-02-19T05:13:48+00:00
url: /go-源码组织方式/
categories:
  - Go
tags:
  - Go

---
Go源码文件以 .go 为后缀。

<pre><code class="line-numbers">Go语言的代码通过包（package）组织，包类似于其它语言里的库（libraries）或者模块（modules）。一个包由位于单个目录下的一个或多个.go源代码文件组成, 目录定义包的作用。每个源文件都以一条package声明语句开始，这个例子里就是package main, 表示该文件属于哪个包，紧跟着一系列导入（import）的包，之后是存储在这个文件里的程序语句。
main包比较特殊。它定义了一个独立可执行的程序，而不是一个库。在main里的main 函数 也很特殊，它是整个程序执行时的入口
</code></pre>

// path 的相对路径 target 是 go 的 build or run 目录 例：
  
var cpath string = &#8220;./config/config.toml&#8221;
  
配置文件使用
  
github.com/BurntSushi/toml
  
所有的struct都定义了才能使用。不好用，推荐 github.com/pelletier/go-toml
  
多个源码文件需要用源码包组织起来。

##### 同一 package 下多文件代码管理

实现：在同一目录下，创建多个 go 文件， 文件的 package 都设置为同一个 package 名。例：package main
  
无需导入文件，直接调用其他文件里的方法。
  
举例：
  
在 mutifiles-package/ 目录下创建两个文件：main.go util.go

<pre><code class="language-go line-numbers">package main
func main(){
foo()
}
// main.go
</code></pre>

<pre><code class="language-go line-numbers">package main
import "fmt"
func foo(){
    fmt.Println("foo()")
    }
// util.go
</code></pre>

命令行执行 `go build`,生成一个 mutifiles-package 可执行文件。
  
`./mutifiles-package` 打印 foo() 。
  
直接运行 `go run main.go util.go` 也可以打印 foo()

* * *

#### 源码文件分三类：

命令源码文件，库源码文件
  
测试源码文件

##### 命令源码文件

声明自己属于 main 代码包、包含无参声明和结果声明的 main 函数。
  
被安装后，相应的可执行文件会被存放到GOBIN 指向的目录或 <当前工作区目录>/bin 下

##### 库源码文件

不具备命令源码文件的那两个特征的源码文件。
  
被安装后，相应的归档文件会被存放到 <当前工作区目录>/pkg<平台相关目录> 下

##### 测试源码文件

不具备命令源码文件的那两个特征的源码文件。
  
文件名称以 _test.go 为后缀
  
测试函数：其中至少有一个函数名以 Test 或 Benchmark 为前缀，并且，该函数接受一个类型为 \*testing.T 或 \*testing.B 的参数

<pre><code class="language-go line-numbers">func TestFind(t *testing.T){
    //功能测试函数
}
func BechmarkFind(t *testing.B){
    //基准测试函数，性能测试函数
}
</code></pre>

##### 代码包的作用

编译和归档Go程序的基本单位。代码划分、集结和依赖的组织形式，也是权限控制的辅助手段。
  
代码包的规则：一个代码包实际上就是一个由导入路径代表的目录。
  
导入路径即 <工作区目录>/src 或 <工作区目录>/pkg/<平台相关路径> 之下的某段子路径

##### 代码包的声明

每个源码文件必须声明其所属的的代码包
  
同一个代码包中的所有源码文件声明的代码包是相同的

##### 代码包声明与代码包导入路径的区别

代码包声明语句中的包名称应该是该代码包的导入路径的最有子路径。
  
例：hypermind.cn/pkgtool <——> package pkgtool

##### 代码包的导入

太多，略。