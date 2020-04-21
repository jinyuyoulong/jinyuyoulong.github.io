---
title: CocoaPods
author: fan
type: post
date: 2019-01-16T03:46:29+00:00
url: /cocoapods/
categories:
  - iOS
  - Mac
  - Xcode
  - 工具

---
* * *title: CocoaPods


  
date: 2016-10-26 10:37:38
  
tags: Cocoapods
  
category: iOS
  
id: 3</p> 

* * *

  * .podspec文件是做什么的

<pre><code class="line-numbers">.podspec文件描述了一个库将怎样被添加进工程中。.podspec文件可以标识该第三方库所需要的源码文件、依赖库、编译选项，以及其他第三方库需要的配置。
</code></pre>

  * Podfile 文件的自述

<pre><code class="line-numbers">  Podfile是用于配置项目所需要的第三方库的地方，使用格式如下：
  platform :ios, '7.0'
  target 'xxx' do
      pod 'AFNetworking', '~&gt; 3.1.0'
      ## react-native (引用本地文件)
      pod 'React', :path =&gt; './node_modules/react-native', :subspecs =&gt; [
          'Core',
      ]
  end
</code></pre>

​