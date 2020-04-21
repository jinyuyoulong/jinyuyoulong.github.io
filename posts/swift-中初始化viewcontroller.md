---
title: swift 中初始化ViewController
categories: [swift]
date: 2016-06-06 18:25:00
---
let vc = NameVC()

    init(title: String){
          super.init(nibName: nil, bundle: nil)
            self.title = title
        }
        required init?(coder aDecoder: NSCoder) {
            fatalError("init(coder:) has not been implemented")
        }