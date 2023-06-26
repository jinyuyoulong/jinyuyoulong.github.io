---
title: "一些对swift语言特性的思考"
date: 2021-04-16T15:39:12+08:00
categories: [iOS,swift]
---

### 数据访问权限

访问控制权限从高到低依次为Open，Public，Internal，File-private，Private。 swift中的访问权限有3层：module层，file层 ，class层 open public internal 对应module层，区别是否可以重写和继承，直接访问。一个APP或一个target可以理解为一个module fileprivate 针对的是file层，对属性和方法的访问权限 private 针对 class层，对子类和extension扩展的访问权限管理 open 可以被任何人使用，包括override重写和继承。 public 可以被任何人访问。但其他module中不可以被override和继承，而在module内可以被override和继承。 internal 默认访问权限，整个App项目内都是可以访问的。 fileprivate所修饰的属性或方法在当前的Swift源文件里可以访问。其他跟private一样。 private所修饰的属性或方法只能在当前类里访问，包括extension。继承的话子类也不能访问。

### let和var的区别

let 是对对象指针的不可变声明，注：对象属性的指针和对象指针没有关系。 var 是对对象指针的可变声明

### 闭包两种声明的区别：前者是值拷贝，后者是指针拷贝，这个没什么可说的，swift语言定的规则

    var thing = "cars"
    let closure = { [thing] in
                   print("I love \(thing)")
                  }
    thing = "airplanes"
    closure()
    

    var thing = "cars"
    let closure = {
      print("I love \(thing)")
    }
    thing = "airplanes"
    closure() // Prints "I love airplanes"
    

#### 在Objective-C中，一个常量可以这样定义：const int number = 0;类似的Swift是这样定义的：let number = 0 两者之间有什么不同吗？如果有，请说明原因。

答案：OC 中 const常量是一个在编译时或者编译解析时被初始化的变量。 通过let创建的是一个运行时常量，是不可变得。他的不可变更多的是c++实现的规则，保证地址内的内容不可更改。 它可以使用static 或者dynamic关键字来初始化。