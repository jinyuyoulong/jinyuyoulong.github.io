---
title: Xcode注释
author: fan
type: post
date: 2016-03-02T07:49:43+00:00
url: /xcode注释/
duoshuo_thread_id:
  - 6278603394835809025
  - 6278603394835809025
categories:
  - iOS

---
## Xcode注释
类与协议

    /** 文档B.
     *
     * 文档B的详细描述.
     */
    @interface DocB : NSObject
    /// 文档A.
    @interface DocA : NSObject


文本链接

    /**
     * - [文档B](DocB) : 类的链接文本.（仅appledoc）
     */


单行注释

    ///# 标题1
    ///## 标题2
    ///hello oc，下面的空行是为了换行
    ///
    ///hello swift
    /// - 这里使用了无序列表
    /// - 使用加粗 **this**， 使用斜体 _this_
    /// - 添加一个链接: [百度](http://www.baidu.com)
    /// - 添加一个图片:![swift picture](http://img0.imgtn.bdimg.com/it/u=14209024,814391630&fm=21&gp=0.jpg )


多行注释文档

    /**
        多行注释文档相比于普通多行注释多了一个星号。
        在这里可以使用markDown语法，书写各种提示信息
        如：显示一个有序列表
        1. 有序列表
        2. 有序列表
        3. 有序列表
    */


方法/函数的注释

方法的注释包括传入参数、返回值、和异常等说明

    /**
     初始化 数据和颜色值
     @param frame      frame
     @param dataItems  数据集
     @param colorItems 色值集
     @return self
     */
     - (id)initWithFrame:(CGRect)frame dataItems:(NSArray*)dataItems colorItems:(NSArray*)colorItems;
#### 在所有的编程环境中 有几种通用的注释方式我们默认遵守他们的规则

它们是：TODO, FIXME, XXX, ??? , !!!

  * 它们分别代表什么意思？ 

> TODO: + 说明：

> 说明在标识处有功能代码待编写，待实现的功能在说明中会简略说明。

> 对那些临时的, 短期的解决方案, 或已经够好但仍不完美的代码使用 TODO 注释.

> FIXME: + 说明：

> 说明标识处代码需要修正，甚至代码是错误的，不能工作，需要修复，如何修正会在说明中简略说明。

> XXX: + 说明：

> 说明标识处代码虽然实现了功能，但是实现的方法有待商榷，希望将来能改进，要改进的地方会在说明中简略说明。 

  * 关于用法
  
    TODO 注释要使用全大写的字符串 TODO, 在随后的圆括号里写上你的大名, 邮件地址, 或其它身份标识. 冒号是可选的. 主要目的是让添加注释的人 (也是可以请求提供更多细节的人) 可根据规范的 TODO 格式进行查找. 添加 TODO 注释并不意味着你要自己来修正.

// TODO(kl@gmail.com): Use a &#8220;*&#8221; here for concatenation operator.

// TODO(Zeke) change this to use relations.

如果加 TODO 是为了在 “将来某一天做某事”, 可以附上一个非常明确的时间 “Fix by November 2005”), 或者一个明确的事项 (“Remove this code when all clients can handle XML responses.”).

  * 如何让Xcode识别这些注释，以便于我们更好的查看？

  1. TARGETS–>(项目名称)–>Build Phases–>选择左上角”+”符号，添加”New Run Script Phase“
  2. 在脚本框中添加
  
    KEYWORDS=”TODO:|FIXME:|???:|!!!:”
  
    find “${SRCROOT}” &#40; -name “.h” -or -name “.m” &#41; -print0 | xargs -0 egrep –with-filename –line-number –only-matching “($KEYWORDS).*$&#8221; | perl -p -e &#8220;s/($KEYWORDS)/ warning: $1/”
  3. 每次编译Xcode时，在Xcode左侧的”show the issue navigator”面板中就能看到你的注释信息