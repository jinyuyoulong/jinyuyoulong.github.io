---
title: go-代码组织方式
date: 2019-02-14 15:48:05
tags:
categories:
  - Go
---

[TOC]

Go源码文件以 .go 为后缀。

Go语言的代码通过**包**（package）组织，包类似于其它语言里的库（libraries）或者模块（modules）。一个包由位于单个目录下的一个或多个.go源代码文件组成, 目录定义包的作用。每个源文件都以一条`package`声明语句开始，这个例子里就是`package main`, 表示该文件属于哪个包，紧跟着一系列导入（import）的包，之后是存储在这个文件里的程序语句。

`main`包比较特殊。它定义了一个独立可执行的程序，而不是一个库。在`main`里的`main` *函数* 也很特殊，它是整个程序执行时的入口

多个源码文件需要用源码包组织起来。

##### 同一 package 下多文件代码管理

实现：在同一目录下，创建多个 go 文件， 文件的 package 都设置为同一个 package 名。但是同一个目录下只能声明一个package name。

例：package main

无需导入文件，直接调用其他文件里的方法。

举例：

在 mutifiles-package/ 目录下创建两个文件：main.go util.go

```go
package main
func main(){
foo()
}
// main.go
```

```go
package main
import "fmt"

func foo(){
    
    fmt.Println("foo()")
    }
// util.go	
```

命令行执行 `go build`,生成一个 mutifiles-package 可执行文件。

`./mutifiles-package` 打印 foo() 。

**注意：**直接运行 `go run main.go util.go` 也可以打印 foo()，必须将两个文件都引入。

---

##### 代码包的导入

### import用法

```
import(
    "fmt"
)
```

上面这个fmt是Go语言的标准库，他其实是去GOROOT下去加载该模块（先找GOROOT，如果GOROOT找不到在去GOPATH找），当然Go的import还支持如下两种方式来加载自己写的模块：

#### 相对路径

```
import "./model"
```

当前文件同一目录的model目录，但是不建议这种方式来import

#### 绝对路径

```
import "shorturl/model"
```

加载gopath/src/shorturl/model模块

#### 点操作

```
import( . "fmt" )
```

这个点操作的含义就是这个包导入之后在你调用这个包的函数时，你可以省略前缀的包名，
也就是前面你调用的fmt.Println(“hello world”)可以省略的写成Println(“hello world”)

#### 别名操作

别名操作顾名思义我们可以把包命名成另一个我们用起来容易记忆的名字

```
import( f "fmt" )
```

别名操作的话调用包函数时前缀变成了我们的前缀，即f.Println(“hello world”)

#### _ 操作

这个操作经常是让很多人费解的一个操作符，请看下面这个import

```go
import ( 
"database/sql" 
_ "github.com/ziutek/mymysql/godrv" 
)
```

_ 操作其实是引入该包，而不直接使用包里面的函数，而是调用了该包里面的init函数。

**main() ,init()方法是go中默认的两个方法，两个保留的关键字。**

init（）方法 是在任何package中都可以出现，但是建议 每个package中只包含一个init()函数比较好，容易理解。

但是main() 方法只能用在package main 中。Go程序会自动调用init()和main()，所以你不需要在任何地方调用这两个函数。

每个package中的init函数都是可选的，但package main就必须包含一个main函数。程序的初始化和执行都起始于main包。如果main包还导入了其它的包，那么就会在编译时将它们依次导入。有时一个包会被多个包同时导入，那么它只会被导入一次（例如很多包可能都会用到fmt包，但它只会被导入一次，因为没有必要导入多次）。当一个包被导入时，如果该包还导入了其它的包，那么会先将其它包导入进来，然后再对这些包中的包级常量和变量进行初始化，接着执行init函数（如果有的话），依次类推。等所有被导入的包都加载完毕了，就会开始对main包中的包级常量和变量进行初始化，然后执行main包中的init函数（如果存在的话），最后执行main函数



下图详细地解释了整个 import 执行过程：

![import 规则](http://static.open-open.com/lib/uploadImg/20131113/20131113222223_265.png)

通过上面的介绍我们了解了import的时候其实是执行了该包里面的init函数，初始化了里面的变量，_ 操作只是说该包引入了，我只初始化里面的 init函数和一些变量，但是往往这些init函数里面是注册自己包里面的引擎，让外部可以方便的使用，就很多实现database/sql的引起，在 init函数里面都是调用了sql.Register(name string, driver driver.Driver)注册自己，然后外部就可以使用了。

#### 命令安装第三方包

```
go get github.com/golang/glog
```

在代码中导入下载的那个第三方包

```go
import (
    "github.com/golang/glog"
)
```

#### 如何让函数供包外使用

 Add() 函数以大写 A 开头，表示将 Add() 函数导出供包外使用。当首字母小写时，为包内使用，包外无法引用到。


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

测试函数：其中至少有一个函数名以 Test 或 Benchmark 为前缀，并且，该函数接受一个类型为 *testing.T 或 *testing.B 的参数

```go
func TestFind(t *testing.T){
    //功能测试函数
}
func BechmarkFind(t *testing.B){
    //基准测试函数，性能测试函数
}
```

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

##### 包的初始化

go语言中init函数用于包(package)的初始化，该函数是go语言的一个重要特性，

有下面的特征：

1 init函数是用于程序执行前做包的初始化的函数，比如初始化包里的变量等

2 每个包可以拥有多个init函数

3 包的每个源文件也可以拥有多个init函数

4 同一个包中多个init函数的执行顺序go语言没有明确的定义(说明)

5 不同包的init函数按照包导入的依赖关系决定该初始化函数的执行顺序

6 init函数不能被其他函数调用，而是在main函数执行之前，自动被调用