---
title: mac下wireshark的使用方法
tags: [Mac,Wireshark]
categories: [system]
date: 2016-05-18 18:47:09
---

Wireshark是mac下一款非常好的抓包工具，安装我就不说了，下面我重点来说说如何使用。
1.打开终端
2.rvictl -s <udid> // 创建一个虚拟接口
3.打开Wireshark，点击设置按钮，选择rvi0接口
4.开始调试

#### 通过 RVI 抓取 iPhone 数据包

（1）RVI 简介
使用 Mac 抓取 iPhone 数据包可通过共享和代理两种方式：
使用 Mac 的网络共享功能将 Mac 的网络通过 WiFi 共享给 iPhone 连接；
使用代理软件（例如 Charles）在Mac上建立HTTP代理服务器。
这两种方式都是将 iPhone 的网络流量导入到 Mac 电脑中，通过 Mac 连接互联网。这就要求 Mac 本身是联网的，对于网络共享的方式还要求 Mac 本身的网络不能使用 WiFi，而且在 iPhone 上只能使用 WiFi 连接，无法抓取到 xG（2G/3G/4G） 网络包。
苹果在 iOS 5 中新引入了“远程虚拟接口（Remote Virtual Interface,RVI）”的特性，可以在 Mac 中建立一个虚拟网络接口来作为 iOS 设备的网络栈，这样所有经过 iOS 设备的流量都会经过此虚拟接口。此虚拟接口只是监听 iOS 设备本身的协议栈（但并没有将网络流量中转到 Mac 本身的网络连接上），所有网络连接都是 iOS 设备本身的，与 Mac 电脑本身联不联网或者联网类型无关。iOS设备本身可以为任意网络类型（WiFi/xG），这样在 Mac 电脑上使用任意抓包工具（tcpdump、Wireshark、CPA）抓取 RVI 接口上的数据包就实现了对 iPhone 的抓包。

# Mac OS X 对 RVI 的支持是通过终端命令 rvictl 提供的，在终端（Terminal）中输入“ rvictl  ? ”命令可查看帮助：

rvictl Options:
           -l, -L                     List currently active devices
           -s, -S                     Start a device or set of devices

#            -x, -X                    Stop a device or set of devices

（2）使用 “ rvictl  -s ”命令创建虚拟接口
首先，通过 MFI USB 数据线将 iPhone 连接到安装了 Mac OS+Xcode 4.2(or later) 的 Mac 机上。iOS 7 以上需要搭配 Xcode 5.0（or later），抓包过程中必须保持连接。
然后，通过 iTunes->Summary 或者 Xcode->Organizer->Devices 获取 iPhone 的 UDID（identifier）。

# 接着，使用“rvictl -s”命令创建 RVI 接口，使用 iPhone 的 UDID 作为参数。

# $rvictl -s <udid>

创建成功后，在终端通过 ifconfig 命令可以看到多了一个 rvi0 接口。当有多个 iOS 设备连接 iMac 时，依次是 rvi1,rvi2…，使用“ rvictl  -l ”命令可以列出所有挂接的虚拟接口。
在 Wireshark 首页选择 rvi0，使用默认的 Capture Options 即可开始对 iPhone 进行抓包。