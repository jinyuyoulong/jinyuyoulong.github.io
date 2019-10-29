---
title: navigationbar status bug
cagegorys: [iOS] 
---

源起：

遇到一个问题，当A->B, A隐藏navigationBar，设置了statusBar的颜色; B反之。

当navigationcontroller短促滑动返回 pop失败的时候，有大概率会出现navigationbar隐藏的bug

原因：这个方法引起的 `- (UIStatusBarStyle)preferredStatusBarStyle`,不改变状态栏颜色的话，这个bug是不会出现的.

解决：导航控制器中重写childViewControllerForStatusBarStyle方法：

```objective-c
-(UIViewController *)childViewControllerForStatusBarStyle{ 
return self.visibleViewController; 
}
```

