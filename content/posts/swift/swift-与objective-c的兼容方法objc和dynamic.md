---
title: Swift与Objective-C的兼容方法:@objc和Dynamic
author: fan
type: post
date: 2016-06-07T02:02:09+00:00
url: /swift与objective-c的兼容方法objc和dynamic/
duoshuo_thread_id:
  - 6293264956431270657
  - 6293264956431270657
categories:
  - swift

---
Swift必须考虑与Objective-C的兼容。
  
首先通过添加{product-module-name}-Bridging-Header.h文件，并在其中填写想要使用的头文件名称，我们就可以很容易地在Swift中使用Objective-C代码了。Xcode为了简化这个设定，甚至在Swift项目中第一次导入Objective-C文件时会主动弹框进行询问是否要自动创建这个文件，可以说是非常方便。
  
但是如果想要在Objective-C中使用Swift的类型的时候，事情就复杂一些。如果是来自外部的框架，那么这个框架与Objective-C项目肯定不是处在同一个target中的，我们需要对外部的Swift module进行导入。这个其实和使用Objective-C的原来的Framework是一样的，对于一个项目来说，外界框架是由Swift写的还是Objective-C写的，两者并没有太大区别。我们通过使用2013年新引入的@import来引入module：
  
[cpp] view plaincopy在CODE上查看代码片派生到我的代码片
  
@import MySwiftKit;
  
之后就可以正常使用这个Swift写的框架了。
  
如果想要在Objective-C里使用的是同一个项目中的Swift的源文件的话，可以直接导入自动生成的头文件{product-module-name}-Swift.h来完成。比如项目的target叫做MyApp的话，我们就需要在Objective-C文件中写：
  
[cpp] view plaincopy在CODE上查看代码片派生到我的代码片
  
#import &#8220;MyApp-Swift.h&#8221;
  
但这只是故事的开始。Objective-C和Swift在底层使用的是两套完全不同的机制，Cocoa中的Objective-C对象是基于运行时的，它从骨子里遵循了KVC（Key-Value Coding，通过类似字典的方式存储对象信息）以及动态派发（Dynamic Dispatch，在运行调用时再决定实际调用的具体实现）。而Swift为了追求性能，如果没有特殊需要的话，是不会在运行时再来决定这些的。也就是说，Swift类型的成员或者方法在编译时就已经决定，而运行时便不再需要经过一次查找，而可以直接使用。
  
显而易见，这带来的问题是如果我们要使用Objective-C的代码或者特性来调用纯Swift的类型时候，我们会因为找不到所需要的这些运行时信息，而导致失败。解决起来也很简单，在Swift类型文件中，我们可以将需要暴露给Objective-C使用的任何地方（包括类，属性和方法等）的声明前面加上@objc修饰符。注意这个步骤只需要对那些不是继承自NSObject的类型进行，如果你用Swift写的class是继承自NSObject的话，Swift会默认自动为所有的非private的类和成员加上@objc。这就是说，对一个NSObject的子类，你只需要导入相应的头文件就可以在Objective-C里使用这个类了。
  
@objc修饰符的另一个作用是为Objective-C侧重新声明方法或者变量的名字。虽然绝大部分时候自动转换的方法名已经足够好用（比如会将Swift中类似init(name: String) 的方法转换成-initWithName:(NSString *)name这样），但是有时候我们还是期望Objective-C里使用和Swift中不一样的方法名或者类的名字，比如Swift里这样的一个类：
  
[cpp] view plaincopy在CODE上查看代码片派生到我的代码片
  
class 我的类 {
      
func 打招呼(名字: String) {
          
println(&#8220;哈喽，&#40;名字)&#8221;)
      
}
  
}
  
我的类().打招呼(&#8220;小明&#8221;)
  
Objective-C的话是无法使用中文来进行调用的，因此我们必须使用@objc将其转为ASCII才能在Objective-C里访问：
  
[cpp] view plaincopy在CODE上查看代码片派生到我的代码片
  
@objc(MyClass)
  
class 我的类 {
      
@objc(greeting:)
      
func 打招呼(名字: String) {
          
println(&#8220;哈喽，&#40;名字)&#8221;)
      
}
  
}
  
这样，我们在Objective-C里就能调用 [[MyClass new] greeting:@&#8221;XiaoMing&#8221;] 这样的代码了（虽然比起原来一点都不好玩了）。另外，正如上面所说的以及在Selector一节中所提到的，即使是NSObject的子类，Swift也不会在被标记为private的方法或成员上自动加@objc。如果我们需要使用这些内容的动态特性的话，我们需要手动给它们加上@objc修饰。
  
添加@objc修饰符并不意味着这个方法或者属性会变成动态派发，Swift依然可能会将其优化为静态调用。如果你需要和Objective-C里动态调用时相同的运行时特性的话，你需要使用的修饰符是dynamic。一般情况下在做App开发时应该用不上，但是在施展一些像动态替换方法或者运行时再决定实现这样的 &#8220;黑魔法&#8221; 的时候，我们就需要用到dynamic修饰符了。在之后的KVO一节中，我们还会提到一个关于使用dynamic的实例。