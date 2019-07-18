---
title: iOS键盘高度的官方获取方法
tags:
  - keyboard
id: 259
categories:
  - iOS
date: 2015-12-02 14:54:36
---

处理键盘事件的正确方法是这样的：（包括获取键盘的高度以及键盘弹出和消失动画的时间）

1）在要使用键盘的视图控制器中，接收键盘事件的通知：
<div class="cnblogs_code">

            [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillShow:) name:UIKeyboardWillShowNotification object:nil];

           [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillHide:) name:UIKeyboardWillHideNotification object:nil];`

    `        // 键盘高度变化通知，ios5.0新增的
    #ifdef __IPHONE_5_0
            float version = [[[UIDevice currentDevice] systemVersion] floatValue];
            if (version &gt;= 5.0) {
                [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillShow:) name:UIKeyboardWillChangeFrameNotification object:nil];
            }
    #endif`</pre>
    <div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a title="复制代码">　　2）然后添加键盘事件的处理代码：</a></span></div>
    </div>
    获取到当前keyboard的高度以及动画时间，然后对视图进行对应的操作即可。
    <div class="cnblogs_code">
    <div class="cnblogs_code_toolbar">
    <pre>`#pragma mark - #pragma mark Responding to keyboard events
    - (void)keyboardWillShow:(NSNotification *)notification {
    /* Reduce the size of the text view so that it's not obscured by the keyboard. Animate the resize so that it's in sync with the appearance of the keyboard. */

     NSDictionary *userInfo = [notification userInfo];

    // Get the origin of the keyboard when it's displayed.
     NSValue* aValue = [userInfo objectForKey:UIKeyboardFrameEndUserInfoKey];

    // Get the top of the keyboard as the y coordinate of its origin in self's view's coordinate system. The bottom of the text view's frame should align with the top of the keyboard's final position.

     CGRect keyboardRect = [aValue CGRectValue];

    // Get the duration of the animation.

     NSValue *animationDurationValue = [userInfo objectForKey:UIKeyboardAnimationDurationUserInfoKey];
     NSTimeInterval animationDuration;
     [animationDurationValue getValue:&amp;animationDuration];

    // Animate the resize of the text view's frame in sync with the keyboard's appearance.
     [self moveInputBarWithKeyboardHeight:keyboardRect.size.height withDuration:animationDuration];
    }

    - (void)keyboardWillHide:(NSNotification *)notification {

     NSDictionary* userInfo = [notification userInfo];

    /* Restore the size of the text view (fill self's view). Animate the resize so that it's in sync with the disappearance of the keyboard. */

     NSValue *animationDurationValue = [userInfo  objectForKey:UIKeyboardAnimationDurationUserInfoKey];
     NSTimeInterval animationDuration;
     [animationDurationValue getValue:&amp;animationDuration];
     [self moveInputBarWithKeyboardHeight:0.0 withDuration:animationDuration];
    }

</div>
<div><a>3）在视图控制器消除时，移除键盘事件的通知：</a></div>
</div>
<div class="cnblogs_code">
<pre>[[NSNotificationCenter defaultCenter] removeObserver:self];</pre>
</div>
ps:

ios5隐藏功能分享——“字典”功能（英英字典）：

在任何输入框中选中一个英文单词，此时会有选择项“复制”，“删除”...等，还有一个向右的箭头，点击这个向右的箭头后，就会出现“定义”选项，点击这个“定义”按钮即会弹出这个英语单词的英文解释。

原文链接

http://www.cnblogs.com/zhulin/archive/2011/10/15/2213687.html