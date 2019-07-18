---
title: CocoaPods
date: 2016-10-26 10:37:38
Tags: ["Cocoapods"]
categories: 
  - iOS
id: 3

---



* .podspec文件是做什么的

```
.podspec文件描述了一个库将怎样被添加进工程中。.podspec文件可以标识该第三方库所需要的源码文件、依赖库、编译选项，以及其他第三方库需要的配置。
```

* Podfile 文件的自述

```
  Podfile是用于配置项目所需要的第三方库的地方，使用格式如下：

  platform :ios, '7.0'

  target 'xxx' do
      pod 'AFNetworking', '~> 3.1.0'

      ## react-native (引用本地文件)
      pod 'React', :path => './node_modules/react-native', :subspecs => [
          'Core',
      ]
  end
```

  ​