---
title: swift 中初始化ViewController
id: 438
categories:
  - swift
date: 2016-06-06 18:25:00
tags:
---

let vc = NameVC()

    init(title: String){
          super.init(nibName: nil, bundle: nil)
            self.title = title
        }

        required init?(coder aDecoder: NSCoder) {
            fatalError("init(coder:) has not been implemented")
        }
    