---
title: "制作framework总结"
date: 2021-05-24T19:15:35+08:00
toc: true
images:
tags: 
  - iOS
---

# ios frameworks 制作总结

## 前提，默认项目已经创建好，代码都有了。

## 更改设置变量

1.  TARGETS —> Build Settings 中设置相关项 （1).Build Active Architecture Only 设置为NO的意思是当前打包的.framework支持所有的设备.否则打包时只能用当前版本的模拟器或真机运行.
2.  Build Setting 搜索linking     设置Dead Code Stripping 为NO是编译选项优化,包瘦身,(可不改)  Mach-O Type 选中StaticLibrary (静态库)  Xcode默认是动态库.
3.  设置framework最低支持的版本
4.  TARGETS —> Build Phases 将需要呈现给来的头文件,直接从Project拖到Public中. 不想呈现出来的.h文件不建议拖到Private中. 放在project中即可
5.  在进行编译之前应该设置为release模式，xcode 左上角 edit scheme
6.  来到工程目录树，Products下的文件都是红色的，现在我们选中.framework文件，分别真机和模拟器运行一遍（成功运行。然后Show in Finder 找到对应的 .framework文件(上级目录可以看出是真机还是模拟器文件夹)
真机和模拟器运行成功的文件是在这俩个文件夹内的

## 合并二进制包

1.  真机版本和模拟器版本framework合并 (1).查看架构信息 打开终端使用命令行 lipo -info 查看framework架构信息 真机版本
2.  合并真机模拟器版本
因为以上获取的framework只能在对应的版本上运行（即真机只能在设备上运行模拟器版本只能在模拟器上面运行使用）所以需要合并为通用版本
命令行语句：lipo -create "真机版本路径" "模拟器版本路径" -output "合并后的文件路径"
`sudo lipo -create release/APPVest simulator/APPVest -output ./APPVest`
3.  检查合并包的架构 lipo -info
然后将合并后的文件替换任意一个framework，release或者simulator的都行。

## 使用

制作好的framework集成使用 把制作好的framework拖入到工程中，引用相关头文件，然后初始化进行暴露方法调用
参考：https://juejin.im/post/5c88e48b6fb9a049d132ff13