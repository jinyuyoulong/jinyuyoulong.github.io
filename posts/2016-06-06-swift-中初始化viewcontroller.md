---
title: swift 中初始化ViewController
author: fan
type: post
date: 2016-06-06T10:25:00+00:00
url: /swift-中初始化viewcontroller/
duoshuo_thread_id:
  - 6293023452072772353
  - 6293023452072772353
categories:
  - swift

---
let vc = NameVC()

    init(title: String){
          super.init(nibName: nil, bundle: nil)
            self.title = title
        }
        required init?(coder aDecoder: NSCoder) {
            fatalError("init(coder:) has not been implemented")
        }