---
title: "Xcode清缓存"
date: 2021-07-08T10:56:53+08:00
draft: false
toc: true
tags: 
  - Xcode
---


列出所有的xcode 模拟器

`xcrun simctl list devices`

`xcrun simctl list devices`

或

`xcrun simctl list --json`
列出所有模拟器

`xcrun simctl delete `

删除特定设备

`xcrun simctl delete unavailable`

删除不再支持的运行时的旧设备

xcrun可以执行更多操作(请参见代码段)

删除完重启xcode
Xcode清理缓存

##### 模拟器

`~/Library/Developer/CoreSimulator`
##### Caches 清空
Devices 保留device_set.plist文件，其余可清空，运行时候可生成

##### Xcode

```sh
~/Library/Developer/Xcode
Archives 这是项目的打包文件，要在移动硬盘做备份，方便后续定位bug用到。
DerivedData 编译的中间文件，可以删除后，重新生成
DocumentationCache 可删除
iOS Device Logs 设备日志，可删除
iOS DeviceSupport 存放的是真机调试的内容
```
测试机
> ~/Library/Developer/XCTestDevices
可清空文件夹
> Playground
> XCPGDevices playground 的项目缓存，可删除

删除Xcode无用的模拟器和架构
> Add and remove simulators only through Xcode > Settings > Components

##### 真机缓存
`private/var/folders/(xx/xx)/com.apple.DeveleperTools/All/Xcode/EmbeddedAppDeltas
/private/var/folders/zt/55wjgcps3qn_mc_3ymr88d5r0000gn/C/com.apple.DeveloperTools/All/Xcode/EmbeddedAppDeltas`

这个文件夹中是真机测试时安装程序的详情，程序猿的Mac如果长期不清理这个文件夹，它能把硬盘的空间吃光。作者：梁间链接：https://www.jianshu.com/p/aad276dc1739来源：简书著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


## Target: Other unnecessary filesPermalink
Path: ~/Library/Caches/..
How: delete each directory
