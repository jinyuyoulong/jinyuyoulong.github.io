---
title: Swift3更改
date: 2016-09-18 13:51:51
tags: [Xcode]
categories: [iOS]
id: 14
---
###  升级Swift3后代码的更改差异
| before                                | after                                   |                                   |
| :------------------------------------ | :-------------------------------------- | --------------------------------: |
| error as NSError                      | error                                   |                                   |
| UIColor().blackColor()                | UIColor().balck                         |                                   |
| xxx.hidden                            | xxx.isHidden                            |                 所有的bool属性，都+前缀：is |
| private                               | fileprivate                             |                                   |
| NSBundle                              | Bundle                                  |                                   |
| func fetchInfo(complete: () -> ()) {} | func fetchInfo(_ complete: () -> ()) {} |        function的参数命名必需添加外部访问参数名或_ |
| setValuesForKeysWithDictionary        | setValuesForKeys                        |                                   |
| MBProgressHUD.hideHUDForView()        | MBProgressHUD.hide(for:)                | for ,with ,of,in 等方法名缩短为(xxx:) 形式 |
| registerClass()                       | register()                              |                                   |
| CGRectMake                            | CGRect()                                |                                   |
| forControlEvents: .TouchUpInside)     | for: .touchUpInside)                    |                              精简命名 |
| NSIndexPath                           | IndexPath                               |                                   |
|                                       |                                         |                                   |
|                                       |                                         |                                   |
|                                       |                                         |                                   |
|                                       |                                         |                                   |
|                                       |                                         |                                   |
|                                       |                                         |                                   |
