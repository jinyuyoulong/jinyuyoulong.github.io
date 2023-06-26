---
title: "制作pod library 私有库"
date: 2020-04-21T13:14:17+08:00
categories: [iOS]
---

[TOC]
## iOS组件化之路——制作pod 私有库

[详细教程点我](https://www.jianshu.com/p/66b63f56b2d5)
1. 创建远程仓库
2. 本地创建项目 pod lib create MyTest
3. 添加文件到Classes/目录下
4. 在example下执行pod update / pod install，安装依赖 ,失败
5. pod lib lint --allow-warnings 验证本地私有库,并忽略警告
6. pod spec lint --allow-warnings 验证远端spec，并忽略警告
7. pod repo push MySpec FFLocalLib.podspec --allow-warnings 私有库加入MySpec版本控制中心并提交到远端
8. end

## 制作 pod 公共库
1. pod lib create MyTest
2. 添加 code
3. 在 example目录下执行 pod install
4. 校验 pod lib lint
5. 注册设备 和邮箱
 pod trunk register xxx@xxx.com 'my name' --description='my macbook air'
6. 邮箱确认注册
7. 提交.podspec pod trunk push MyTest.podspec
8. 搜索自己的库 pod search MyTest 由于墙的原因可能不会马上可以搜到

[参考制作自己的cocoapods](https://www.jianshu.com/p/c94d394f0be7)