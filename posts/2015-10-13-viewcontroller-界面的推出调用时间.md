---
title: ViewController 界面的推出调用时间
author: fan
type: post
date: 2015-10-13T02:22:27+00:00
url: /viewcontroller-界面的推出调用时间/
duoshuo_thread_id:
  - 6278603346337071874
  - 6278603346337071874
categories:
  - iOS

---
ViewController 界面的推出，是在ViewDidLoad方法运行之后才被推出的，

所以说，ViewWillAppear和ViewDidAppear 是在ViewDidLoad之后调用的。