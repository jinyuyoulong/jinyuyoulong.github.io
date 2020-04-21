---
title: Xcode Code Snippets
author: fan
type: post
date: 2018-09-18T11:50:09+00:00
excerpt: 通过code snippets，我们可以创建一些可重用的代码块，并且在任何需要的地方很容易的就可以使用这些代码块。这可以节省输入需要的操作和时间。并且，一旦你学会使用code snippets，会发现你可
url: /xcode-code-snippets/
categories:
  - Xcode
tags:
  - xcode

---
Xcode Code Snippets
  
在Double Encore，我们写的代码都是干净，可重用的——不过，有时候并不能完全做到。如在使用pragma mark的时候。下面就是一个示例：
  
#pragma mark &#8211; UIViewController overrides
  
通过pragma mark，可以让代码看起来既整洁又有组织。虽然这很重要，但是会带来额外的输入操作和时间。此时，我们可以使用code snippets。
  
通过code snippets，我们可以创建一些可重用的代码块，并且在任何需要的地方很容易的就可以使用这些代码块。这可以节省输入需要的操作和时间。并且，一旦你学会使用code snippets，会发现你可以创建并扩充自己的code snippet library。
  
创建一个code snippet非常简单。首先，打开Xcode并在utilities panel中选择code snippet library。
  
上图中，可以看到在code snippet library中已经有一些数据了。
  
接着，输入希望创建的code snippet。在这里，我为pragma mark创建一个code snippet。如下图所示，在代码编辑器中输入 “#pragma mark – UIViewController overrides”。
  
选中代码块，如下图所示：
  
然后单击并按住代码块，知道文本光标变为箭头光标。接着将代码块拖放到code snippet library中，然后松开鼠标。如下图所示
  
此时会弹出一个popover，通过该popover可以对新的code snippet进行编辑，如下图所示。
  
首先，是定snippet的名字。这里我指定为“Pragma Mark”
  
然后，指定该snippet的completion shortcut（可选项）。这里我指定为“pm”。这样设置以后，在Xcode的代码编辑器中只需要输入快捷方式（pm），就能简单的将这个snippet添加到代码中。非常有用！
  
接着，可以看到在上面的示例中，pragma mark的标题是“UIViewController overrides”，不过我们是希望对其修改一下，以能够很容易的输入任意标题。
  
我们可以简单的将code snippet包含的文本内容修改为“#pragma mark – “即可。不过，这里还有更好的一个办法——将文本块封装到“<#” 和 “#>”中间，这样code snippet将指出我们可以插入自定义文本的完整范围。
  
下面，将“UIViewController overrides”替换为“<#Title#>”。
  
注意，completion scopes字段在这里并没有做修改，通过该字段可以指定completion shortcut的有效范围。
  
最后，点击edit按钮，以完成snippet的编辑。之后可以在这个popover画面中看到最终结果的一个预览效果。
  
然后点击popover中的done按钮。下面，你可以将我们在代码编辑器中为创建snippet而写入的文本行删除掉。
  
现在来试用一下刚刚创建的snippet！有两种方法。第一种是在code snippet library中找到snippet，然后用鼠标将其拖拽到代码编辑器中…
  
&#8230;然后松开鼠标。
  
一旦将snippet拖放到代码编辑器之后，就可以通过点击键盘上的tab键在不同的completion字段间移动焦点。
  
第二种方法是在代码编辑器里简单的输入completion shortcut中设置的内容即可。我们这里是“pm”。
  
然后点击键盘中的return键，就可以将snippet插入到代码编辑器中。
  
很简单吧！现在你已经知道如何创建自己的snippet了，你将发现这非常的有用。任何时候，你都遇到重复输入的相同代码块，都可以考虑将其添加到你的code snippets library中。
  
下面是我经常使用到的一些snippet：
  
Title: Animation Block
  
Completion Shortcut: ab
  
Completion Scopes: Function or Method
  
void (^<#Title#>)(void) = ^{ };
  
Title: Animation Completion Block
  
Completion Shortcut: acb
  
Completion Scopes: Function or Method
  
void (^<#Title#>)(BOOL) = ^(BOOL finished) { };
  
Title: Notification Add
  
Completion Shortcut: na
  
Completion Scopes: Function or Method
  
[[NSNotificationCenter defaultCenter] addObserver:<#Observer#> selector:<#Selector#> name:<#Name#> object:<#Object#>];
  
Title: Notification Remove
  
Completion Shortcut: nr
  
Completion Scopes: Function or Method
  
[[NSNotificationCenter defaultCenter] removeObserver:<#Observer#> name:<#Name#> object:<#Object#>];
  
Title: NSLog
  
Completion Shortcut: log
  
Completion Scopes: Function or Method
  
NSLog(@&#8221;<#Log#>&#8221;);
  
Title: Private Interface
  
Completion Shortcut: pi
  
Completion Scopes: Top Level
  
@interface <#Title#> ()
  
@end
  
Title: Property Assign
  
Completion Shortcut: pa
  
Completion Scopes: All
  
@property (assign, nonatomic)
  
Title: Property Strong
  
Completion Shortcut: ps
  
Completion Scopes: All
  
@property (strong, nonatomic)
  
Title: Property Unsafe Unretained
  
Completion Shortcut: pu
  
Completion Scopes: All
  
@property (unsafe_unretained, nonatomic)
  
来源http://www.cocoachina.com/industry/20130604/6336.html