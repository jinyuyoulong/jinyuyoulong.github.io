---
title: "Xcode清缓存"
date: 2021-07-08T10:56:53+08:00
draft: false
toc: true
tags: 
  - Xcode
---
文章引自-[  Clean up Xcode cache files on your Mac](
https://lovemewithoutall.github.io/it/xcode-clean-up/)

 less than 1 minute read
There is no side effect. I got 100Gb!

## Target: unused devicePermalink
Path: ~/Library/Developer/CoreSimulator/Devices
How: execute command on terminal xcrun simctl delete unavailable
Path: ~/Library/Developer/Xcode/iOS DeviceSupport
How: delete directorys like ‘9.0.0’
## Target: unnecessary filesPermalink
Path: ~/Library/Developer/CoreSimulator/Caches/dyld/..
How: delete each directory
## Target: builded App cachesPermalink
Path: ~/Library/Developer/Xcode/DerivedData
How: delete each directory
## Target: unnecessary ArchivesPermalink
Path: ~/Library/Developer/Xcode/Archives
How: delete each directory
## Target: logsPermalink
Path: ~/Library/Developer/Xcode/iOS Device Logs
How: delete each directory
## Target: Other unnecessary filesPermalink
Path: ~/Library/Caches/..
How: delete each directory
