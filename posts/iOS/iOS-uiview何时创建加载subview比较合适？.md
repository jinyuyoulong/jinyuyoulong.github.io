---
title: UIView何时创建加载subview比较合适？
categories: [iOS]
date: 2016-03-07 15:38:43
---
当我们使用ViewController的时候有ViewDidLoad方法保证数据或UI只加载一次

但是在UIView中 没有这样的生命周期函数 如果你的subview的创建是这样写的

    - (instancetype)initWithFrame:(CGRect)frame
    {
        self = [super initWithFrame:frame];
        if (self) {
            [self makeView];
        }
        return self;
    }


那么恭喜你 你的代码很可能会出问题 因为我发现 `initWithFrame`会调用两次，不要问我为什么，我也不知道

所以应该在哪里创建呢？

这时我想起来了tableView的delegate方法，是一组按顺序执行的接口方法，啊哈，这是个很好的解决方案。

我们可以对外暴露一个方法， 当View初始化完成之后 在调用创建subview的方法

想在那里执行就在那里执行，想什么时候创建就什么时候创建