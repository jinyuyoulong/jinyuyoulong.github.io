---
title: iOS8.3发布了Swift 1.2带来哪些新变化
id: 18
categories: [iOS]
date: 2015-04-14 14:59:50
tags: [iOS]
---

原文&nbsp;&nbsp;[http://www.cnblogs.com/yuyongjian/p/4371400.html](http://www.cnblogs.com/yuyongjian/p/4371400.html?utm_source=tuicool)

![](http://img2.tuicool.com/2EjEfe.jpg "1423710600589982.jpg")

苹果前几日在面向开发者推送iOS 8.3 Beta的同时，还发布了版本号为6D520o的Xcode 6.3 Beta，其中便包含了iOS 8.3 Beta和OS X v10.10 SDK，并进一步提升了Swift与Objective-C代码的交互性，而Swift业已更新至1.2版本。@未来眼之老码团队第一时间翻译了完整的Release Note。共计50多处改动，同时修改了Objective-c的语法，足见苹果对Swift语言的重视。

![](http://img2.tuicool.com/MBZzA3.jpg "1423710718209509.jpg")

从&nbsp;[Xcode 6.3 Beta Release Notes](https://developer.apple.com/unauthorized/)&nbsp;看出，Xcode 6.3 Beta包含了很多颇为值得开发者期待的改变，共计50多处改动，同时修改了Objective-C的语法，足见苹果对Swift语言的重视。而其代码迁移工具可以帮助开发者将其代码从Swift 1.1（Xcode 6.1）升级至Swift 1.2（Xcode 6.3），具体执行编辑菜单（Edit）-&gt;转换（Convert）-至（To）Swift1.2即可。 具体更新如下：

Swift语言的增强

*   Swift现在支持目标增量编译，例如当一个文件改变时不会重新编译Target中的每一个文件。这个基于固有依赖分析。所以你依然会看到有很多文件在必要情况下被重编。如果你发现需要重编但没有重编的情况，请报一个Bug出来。清理Target后再编，会按照往常的流程进行。

*   增加了一个新的Set数据类型，它提供了元素唯一化，且有完整语义的通用数据类型集合。它和NSSet类型桥接，提供和Array和Dictionary相类似的功能。

*   if let语句现在被扩展为可以支持多条条件判断：<pre>if&nbsp;let&nbsp;a&nbsp;=&nbsp;foo(),&nbsp;b&nbsp;=&nbsp;bar()&nbsp;where&nbsp;a&nbsp;&lt;&nbsp;b,&nbsp;&nbsp;
let&nbsp;c&nbsp;=&nbsp;baz()&nbsp;{&nbsp;&nbsp;
&nbsp;}</pre>

它允许你测试多种选择，并且包含一个bool判断。当然这种情况不包含嵌套判断。

let常量现在生成时不需要立即初始化，新的规则是let常量必须在被首次使用前初始化即可（和var一样）。或者说它只能被初始化，也就是说在初始化后它不能再被改变或者重新赋值，可用的模式如下：
<pre>let&nbsp;x:&nbsp;SomeThing&nbsp;&nbsp;
&nbsp;if&nbsp;condition&nbsp;{&nbsp;&nbsp;
&nbsp;x&nbsp;=&nbsp;foo()&nbsp;&nbsp;
&nbsp;}&nbsp;else&nbsp;{&nbsp;&nbsp;
&nbsp;x&nbsp;=&nbsp;bar()&nbsp;&nbsp;
&nbsp;}&nbsp;&nbsp;
&nbsp;use(x)</pre>

这个正常的来说需要var变量用法，尽管这里没有任何修改的操作。

*   “Static”静态方法和属性现在允许在class中使用(作为“class final”的别名)。你现在可以在类中声明一个静态存储属性，它享有全局存储空间和首次使用再初始化的惰性构造功能。协议Protocal现在会声明一个static的类型要求而不是声明一个class的要求。

*   对于表达式闭包的类型引用有了几点改进：

1.  含有单返回语句的闭包现在类型检查时以单表达式闭包处理。

2.  匿名的且含有非空返回类型的单表达式现在可以用在Void上下文中。

3.  多表达式的闭包类型的情况可能无法被类型推断出来，这归功于缺乏返回类型的情况能被正确的推断出来。

*   Swift中的枚举类型现在可以通过@objc关键字导出到Objective-C中。@objc的枚举类型必须定义一个整型的原始类型，并且该枚举不能泛型化或者不能使用关联值。由于Objective-C中的枚举类型没有命名空间，所以导出到Objective-C中的枚举类型以枚举名字和case项目名字的组合的方式使用。 比如在Swift中的声明：<pre>@objc&nbsp;&nbsp;
&nbsp;enum&nbsp;Bear:&nbsp;Int&nbsp;{&nbsp;&nbsp;
&nbsp;case&nbsp;Black,&nbsp;Grizzly,&nbsp;Polar&nbsp;&nbsp;
&nbsp;}</pre>

导出到Objective-C：
<pre>typedef&nbsp;NS_ENUM(NSInteger,&nbsp;Bear)&nbsp;{&nbsp;&nbsp;
BearBlack,&nbsp;BearGrizzly,&nbsp;BearPolar&nbsp;&nbsp;
};</pre>

*   Objective-C语言的扩展语法现在可以判断出Objective-C API中指针或者block的是否为空，同时允许不带ImplicitlyUnwrappedOptional协议地导出Objective-C API函数。

*   Swift现在可以部分支持导入C的联合类型，包括unions、bitfileds、SIMD vector类型以及其他Swift的不支持的C特性。这些不被支持的元素不能在Swift中的直接访问，但是在Swift中，Objective-C或者C可以以参数或者返回类型的方式使用。这包括Foundation NSDecimal类型、GLKit GLKVector和GLKMatrix类型，以及其他一些类型。

*   被导入的C结构体现在在Swift中有一个默认的构造器，它会将结构体中的所有的元素初始化为0，例如：<pre>import&nbsp;Darwin&nbsp;&nbsp;
&nbsp;var&nbsp;devNullStat&nbsp;=&nbsp;stat()&nbsp;&nbsp;
&nbsp;stat(&quot;/dev/null&quot;,&nbsp;&amp;devNullStat)</pre>

如果一个结构体的元素不能被正确的初始化为0（比如被标记为新的_nonnull标示符时），这个默认的构造器将会终止。

*   String的索引类型间新的转换API现在可以用了，如String、String.UnicodeScalarView、String.UTF16View以及String.UTF8View， 同时每个String View转换为String的函数也可使用。

*   类型值在println函数或者字符串内插算法中现在可以打印完整的类型名称了：<pre>toString(Int.self)&nbsp;//&nbsp;打印&nbsp;“Swift.Int&quot;&nbsp;&nbsp;
&nbsp;println([Float].self)&nbsp;//&nbsp;打印&nbsp;&quot;Swift.Array”&nbsp;&nbsp;
&nbsp;println((Int,&nbsp;String).self)&nbsp;//&nbsp;打印&nbsp;&quot;(Swift.Int,&nbsp;Swift.String)&quot;</pre>

*   一个新的“@noescape”属性可以用在函数的闭包参数上，这意味着这个参数是唯一可被调用的（或者用在函数调用时以参数的方式出现），其意思是它的生命周期比函数调用的周期短，这有助于一些小小的性能优化，但最重要的是它屏蔽了闭包中对self.的需求。这使得函数的控制流比其他更加透明。在未来的beta版本中，标准库函数将普遍采用这种特性，比如autoreleasepool()：<pre>func&nbsp;autoreleasepool(@noescape&nbsp;code:&nbsp;()&nbsp;-&gt;&nbsp;())&nbsp;{&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;pushAutoreleasePool()&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;code()&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;popAutoreleasePool()&nbsp;&nbsp;
&nbsp;}</pre>

*   相比Swift 1.1，Swift 1.2在很多方面的性能上有本质的提高，比如多维数组算法更快，未优化的代码更加快速。

*   表达式类型的错误诊断有了很大的提高。

*   很多通用表达式的检查效率有很大提高，这个有助于降低编译时间和减少“expression too complex”的错误。

Swift语言的改变

*   “确保转换”和“可失败转换”的概念现在被分为两个操作符。可失败转换现在使用as!运算符，这个！感叹号可以让代码的读者更清晰的明白本次转换可能失败并触发一个运行时错误。“as”操作符会保持向上转换（比如“someDerivedValue转换为Base”）或者类型标注（“0 转换为Int8”），它保证了转换不会失败。

*   结构体和类构造器中的let不可变属性现在被规范为更加标准的通用模型：lets类型初始化后将永不会被改变或重新赋值。以前的实现是，可以在构造器中任意修改，而现在它们只允许被初始化和提供值操作。如果一个属性在声明时已经赋值，那么它会被所有的构造器认为已经含有初始值。

*   从桥接Objective-C类 (NSString/NSArray/NSDictionary）到它Swift中值类型的隐式转化被移除。这将是Swift的类型系统更加简单和可预测。这意味着：<pre>import&nbsp;Foundation&nbsp;&nbsp;
func&nbsp;log(s:&nbsp;String)&nbsp;{&nbsp;println(x)&nbsp;}&nbsp;&nbsp;
let&nbsp;ns:&nbsp;NSString&nbsp;=&nbsp;&quot;some&nbsp;NSString&quot;&nbsp;//&nbsp;Okay&nbsp;&nbsp;
log(ns)&nbsp;//&nbsp;错误&nbsp;&nbsp;
//&nbsp;&quot;&#39;NSString&#39;&nbsp;不能转换为&nbsp;&#39;String&#39;&quot;</pre>

为了完成桥接转换，需要用显式转化符标注：
<pre>log(ns&nbsp;as&nbsp;String)&nbsp;//&nbsp;succeeds</pre>
从Swift类型到Objective-C类型的桥接隐式转换依然被允许，比如：
<pre>func&nbsp;nsLog(ns:&nbsp;NSString)&nbsp;{&nbsp;println(ns)&nbsp;}&nbsp;&nbsp;
&nbsp;let&nbsp;s:&nbsp;String&nbsp;=&nbsp;“some&nbsp;String”&nbsp;&nbsp;
&nbsp;nsLog(s)&nbsp;//&nbsp;okay:&nbsp;implicit&nbsp;conversion&nbsp;from&nbsp;String&nbsp;to&nbsp;NSString&nbsp;is&nbsp;still&nbsp;permitted</pre>

*   @autoclosure现在标注在参数上，而不是标注在参数的类型上。比如：<pre>//以前我们这样写：&nbsp;&nbsp;
&nbsp;func&nbsp;assert(predicate&nbsp;:&nbsp;@autoclosure&nbsp;()&nbsp;-&gt;&nbsp;Bool)&nbsp;{…&nbsp;}&nbsp;&nbsp;
//现在需要这样写：&nbsp;&nbsp;
&nbsp;func&nbsp;assert(@autoclosure&nbsp;predicate&nbsp;:&nbsp;()&nbsp;-&gt;&nbsp;Bool)&nbsp;{…&nbsp;}</pre>

*   使用在函数参数上的 @autoclosure属性现在含有@noescape新属性的功能，这个改进限制了@autoclosure作为控制流程以及惰性计算的能力。

*   柯里化函数现在可以指定参数标签了：<pre>func&nbsp;curryUnnamed(a:&nbsp;Int)(_&nbsp;b:&nbsp;Int)&nbsp;{&nbsp;return&nbsp;a&nbsp;+&nbsp;b&nbsp;}&nbsp;&nbsp;
curryUnnamed(1)(2)&nbsp;&nbsp;
func&nbsp;curryNamed(first&nbsp;a:&nbsp;Int)(second&nbsp;b:&nbsp;Int)&nbsp;-&gt;&nbsp;Int&nbsp;{&nbsp;return&nbsp;a&nbsp;+&nbsp;b&nbsp;}&nbsp;&nbsp;
curryNamed(first:&nbsp;1)(second:&nbsp;2)</pre>

*   Swift现在可以检测在Swift类型系统中覆盖和重写的差异以及通过Objective-C运行时可见的影响。比如，下面Objective-C类中对属性的setter和类扩展中对方法的“setProperty”它们之间的冲突现在可以被诊断：<pre>class&nbsp;A&nbsp;:&nbsp;NSObject&nbsp;{&nbsp;&nbsp;
&nbsp;var&nbsp;property:&nbsp;String&nbsp;=&nbsp;&quot;Hello&quot;&nbsp;//&nbsp;注意:&nbsp;Objective-C&nbsp;方法&nbsp;&#39;setProperty:’&nbsp;&nbsp;
&nbsp;//&nbsp;以前这里“属性”这里是通过setter声明&nbsp;&nbsp;
&nbsp;}&nbsp;&nbsp;
&nbsp;extension&nbsp;A&nbsp;{&nbsp;&nbsp;
&nbsp;func&nbsp;setProperty(str:&nbsp;String)&nbsp;{&nbsp;}&nbsp;//&nbsp;错误：方法&quot;setProperty&quot;&nbsp;&nbsp;
&nbsp;//&nbsp;重复声明了Objective-C方法&nbsp;&nbsp;
&nbsp;//&#39;setProperty:&#39;&nbsp;&nbsp;
&nbsp;}</pre>

同样地检查在Objective-C中重写：
<pre>class&nbsp;B&nbsp;:&nbsp;NSObject&nbsp;{&nbsp;&nbsp;
func&nbsp;method(arg:&nbsp;String)&nbsp;{&nbsp;}&nbsp;//&nbsp;注意：重写操作&nbsp;&nbsp;
//&nbsp;这里含有类型：&#39;(String)&nbsp;-&gt;&nbsp;()&#39;&nbsp;&nbsp;
}&nbsp;&nbsp;
class&nbsp;C&nbsp;:&nbsp;B&nbsp;{&nbsp;&nbsp;
func&nbsp;method(arg:&nbsp;[String])&nbsp;{&nbsp;}&nbsp;//&nbsp;错误:&nbsp;重写的选择器方法含有不匹配的类型&#39;([String])&nbsp;-&gt;&nbsp;()&#39;&nbsp;&nbsp;
}</pre>

和协议的适配性一样：
<pre>class&nbsp;MyDelegate&nbsp;:&nbsp;NSObject,&nbsp;NSURLSessionDelegate&nbsp;{&nbsp;&nbsp;
&nbsp;func&nbsp;URLSession(session:&nbsp;NSURLSession,&nbsp;didBecomeInvalidWithError:&nbsp;Bool){&nbsp;}&nbsp;&nbsp;
&nbsp;//&nbsp;错误：Objective-C&nbsp;方法&nbsp;&#39;URLSession:didBecomeInvalidWithError:&#39;&nbsp;&nbsp;
&nbsp;//由方法提供：&nbsp;&#39;URLSession(_:didBecomeInvalidWithError:)&#39;&nbsp;&nbsp;
&nbsp;//&nbsp;和可选类型的需求方法相冲突：&nbsp;&nbsp;
&nbsp;//&nbsp;&#39;URLSession(_:didBecomeInvalidWithError:)&#39;&nbsp;在协议&nbsp;&nbsp;
&nbsp;//&nbsp;&#39;NSURLSessionDelegate&#39;&nbsp;&nbsp;
&nbsp;}</pre>

Swift语言Bug修复

*   动态转换符(“as!”, “as?“和“is”)现在可以用在Swift的协议类型上，只要该协议类型没有关联类型。

*   在Playground增加的一致性需求现在可以按照预期工作了，比如：<pre>struct&nbsp;Point&nbsp;{&nbsp;&nbsp;
&nbsp;var&nbsp;x,&nbsp;y:&nbsp;Double&nbsp;&nbsp;
&nbsp;}&nbsp;&nbsp;
&nbsp;extension&nbsp;Point&nbsp;:&nbsp;Printable&nbsp;{&nbsp;&nbsp;
&nbsp;var&nbsp;description:&nbsp;String&nbsp;{&nbsp;&nbsp;
&nbsp;return&nbsp;&quot;((x),&nbsp;(y))&quot;
&nbsp;}&nbsp;&nbsp;
&nbsp;}&nbsp;&nbsp;
&nbsp;var&nbsp;p1&nbsp;=&nbsp;Point(x:&nbsp;1.5,&nbsp;y:&nbsp;2.5)&nbsp;&nbsp;
&nbsp;println(p1)&nbsp;//&nbsp;prints&nbsp;&quot;(1.5,&nbsp;2.5)”</pre>

*   导入的没有文档化的NS_ENUM类型，比如UIViewAnimationCurve，现在可以通过init(rawValue:) 构造器从它的原始整型类型转换出来而不会重设为nil，为解决这个问题而用替代方法unsafeBitCast编写的代码现在可以使用原始值构造器编写了。比如：<pre>let&nbsp;animationCurve&nbsp;=&nbsp;&nbsp;
nsafeBitCast(userInfo[UIKeyboardAnimationCurveUserInfoKey].integerValue,&nbsp;&nbsp;
UIViewAnimationCurve.self)</pre>

现在可以写为：
<pre>let&nbsp;animationCurve&nbsp;=&nbsp;UIViewAnimationCurve(rawValue:&nbsp;&nbsp;
userInfo[UIKeyboardAnimationCurveUserInfoKey].integerValue)!</pre>

*   在枚举类型中负浮点数可以用作原始值了。

*   指向Objective-C类，或者Swift中继承自Objective-C对象的无主引用，在该无主引用指向的对象释放后无主引用被重新赋值时不会再Crash。

*   含有观察访问器的变量或者属性如果它可以从初始值表达式中推断出类型就无需显式指定类型。

*   NSClassFromString函数搜索失败时其结果和nil的比较现在工作正常。

*   子类中的重写基类含有可选类型的方法时，如果涉及到可选类型的转换将不会导致Crash。<pre>class&nbsp;Base&nbsp;{&nbsp;&nbsp;
&nbsp;func&nbsp;foo(x:&nbsp;String)&nbsp;-&gt;&nbsp;String?&nbsp;{&nbsp;return&nbsp;x&nbsp;}&nbsp;&nbsp;
&nbsp;}&nbsp;&nbsp;
&nbsp;class&nbsp;Derived:&nbsp;Base&nbsp;{&nbsp;&nbsp;
&nbsp;override&nbsp;func&nbsp;foo(x:&nbsp;String?)&nbsp;-&gt;&nbsp;String&nbsp;{&nbsp;return&nbsp;x!&nbsp;}&nbsp;&nbsp;
&nbsp;}</pre>

关于Objective-C语言的增强

Objective-C API中可以表示参数，返回值，属性，变量等等的“nullability”属性。比如，下面是表达很多UITableView API的为空特性：
<pre>-(void)registerNib:(nonnull&nbsp;UINib&nbsp;*)nib&nbsp;forCellReuseIdentifier:(nonnull&nbsp;&nbsp;
SString&nbsp;*)identifier;&nbsp;&nbsp;
-(nullable&nbsp;UITableViewCell&nbsp;*)cellForRowAtIndexPath:(nonnull&nbsp;&nbsp;
SIndexPath)indexPath;&nbsp;&nbsp;
@property&nbsp;(nonatomic,&nbsp;readwrite,&nbsp;retain,&nbsp;nullable)&nbsp;UIView&nbsp;*backgroundView;</pre>

这个nullability标示符影响了Objective-C API在Swift的可选类型值，nonnull标示符标示的类型将会以非可选的类型的导入，这个用来替代隐式解封可选类型如(e.g., UINib!）。而nullable标示符标示的类型则会以可选类型导入（如UITableViewCell?），所以下面的API在Swift中表现如下：
<pre>func&nbsp;registerNib(nib:&nbsp;UINib,&nbsp;forCellReuseIdentifier&nbsp;identifier:&nbsp;String)&nbsp;&nbsp;
func&nbsp;cellForRowAtIndexPath(indexPath:&nbsp;NSIndexPath)&nbsp;-&gt;&nbsp;UITableViewCell?&nbsp;&nbsp;
var&nbsp;backgroundView:&nbsp;UIView?</pre>

可空特性标示符也可以用在指针类型，包括C指针，block指针和C++成员指针，使用双下划线方式，比如：
<pre>void&nbsp;enumerateStrings(__nonnull&nbsp;CFStringRef&nbsp;(^&nbsp;__nullable&nbsp;callback)(void));</pre>
这里，它自身的回调函数是nullable的，但是它的回调函数的返回类型为nonnull，所以这个API在Swift以如下方式使用：
<pre>func&nbsp;enumerateStrings(callback:&nbsp;(()&nbsp;-&gt;&nbsp;CFString)?)</pre>
总的来说，可空特性标示符有三种，可以用双下划线（用在任何指针类型），或者没有下划线的（用在Objective-C属性，方法结果类型或者方法参数类型）。

![](http://img0.tuicool.com/MjeInmR.jpg "1423711358267173.jpg")

*   特别是在Objective-C API中，很多指针倾向于nonnull，因此Objective-C提供了“audited”域（通过新的#pragma），它会认为未被标注的指针为nonnull，比如下面的例子等同于上面第一个例子，但是它用的是“audited”域来简化语句表达：<pre>#pragma&nbsp;clang&nbsp;assume_nonnull&nbsp;begin&nbsp;&nbsp;
&nbsp;//&nbsp;…&nbsp;&nbsp;
&nbsp;-(void)registerNib:(UINib&nbsp;*)nib&nbsp;forCellReuseIdentifier:(NSString&nbsp;&nbsp;
*)identifier;&nbsp;&nbsp;
&nbsp;-(nullable&nbsp;UITableViewCell&nbsp;*)cellForRowAtIndexPath:(NSIndexPath)indexPath;&nbsp;&nbsp;
&nbsp;@property&nbsp;(nonatomic,&nbsp;readwrite,&nbsp;retain,&nbsp;nullable)&nbsp;UIView&nbsp;*backgroundView;&nbsp;&nbsp;
&nbsp;//&nbsp;…&nbsp;&nbsp;
&nbsp;#pragma&nbsp;clang&nbsp;assume_nonnull&nbsp;end</pre>

*   为了保证代码的连续性，我们强烈建议你在所有的Objective-C头文件使用“audited”域来表述其api的可空性，同时避免null_unspecified情况，建议使用在将可空性引入到现有的头文件时采用该功能作为过渡工具。

*   Objective-C增加的nullability注解不会影响它的向后兼容性也不会影响代码的编译。比如nonnull在有些情况下依然可以以nil结束，诸如消息路由到一个为nil的接收器，但是，nullability注解只是提高Swift的编程体验，它会在Objective-C中产生一个新的警告，诸如朝一个nonnull的参数赋一个nil的话，这使得Objective-c API更加高效以及使用的正确。

*   Objective-C可以通过null_resettable来表达属性的空属性，该属性setter访问器允许将其设置为nil（设置该属性为默认值），但是它的getter访问器不会提供一个nil值（因为它提供了默认值），有一个这样的属性如UIView’s tintColor，如果没有tint颜色指定时它会提供一个默认的tint颜色值，如：<pre>@property&nbsp;(nonatomic,&nbsp;retain,&nbsp;null_resettable)&nbsp;UIColor&nbsp;*tintColor;</pre>

这样的API在Swift使用隐式强制解封的方法使用：
<pre>var&nbsp;tintColor:&nbsp;UIColor!</pre>
C指针类型的参数或者Block指针类型可以使用noescape新属性标志，它用来标明这个指针参数不会离开这个函数或者方法而使用。这种情况下，可以安全的传递一个局部变量地址，noescape block指针在Swift中将会被映射为@noescape参数：
<pre>void&nbsp;executeImmediately(__attribute__((noescape))&nbsp;void&nbsp;(^callback)(void);</pre>
将被影射到Swift为：
<pre>func&nbsp;executeImmediately(@noescape&nbsp;callback:&nbsp;()&nbsp;-&gt;&nbsp;Void)</pre>
*   LLDB现在包含了一个printf()函数去计算C/C++/Objective-C表达式，这个将在arm64设备上提升表达式计算的体验，但是可能和用户在.lldbinit定义的表达式前缀冲突，如果你发现在表达式计算时出现错误，这可能就是root cause。

*   XCode 6.3将Apple LLVM编译器更新为6.1.0，这个新的编译器版本包含了对C++14标准的全部支持，包括大量的增强的警告诊断和新的优化，对于arm64架构的支持进行了有效的重构来支持ARM的实现， 这个将明显影响矩阵内联函数计算。

*   为arm64 vfma/vfms内联函数预定的参数被移除，虽然这个改变不会产生一个编译时错误，但是它会中断代码运行时操作，我们需要明确这个变化来减少风险。默认的，编译器现在会对使用这种内联属性提供警告并维持固有的行为，在尽可能的情况下，你需要接受这个变化并且定义USE_CORRECT_VFMA_INTRINSICS宏为1告诉编译器接收警告，当然你也可以可以USE_CORRECT_VFMA_INTRINSICS宏为0来屏蔽警告并保持固有行为。但是请不要保留这样的代码太久，因为我们计划在未来的版本中移除对这种旧行为的支持。

*   含有自动尺寸标志的视图以及包含在UITableView、UICollectionView或NSScrollView的视图在打开文档时不会再出现对齐错误。

*