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
### podspec文件是做什么的

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
### readme文件如何添加

[![Liberapay patrons][1]][1]这种说明

  1. 打开网站https://shields.io/#/examples/funding
  2. 选择flat Style
  3. 在Link和Image中输入http://img.shields.io/cocoapods/v/库名称.svg，网站会自动解析库的版本，生成img
  4. copy下面的Markdown，paste到要显示说明的地方

[1]: http://img.shields.io/cocoapods/v/FFKit.svg