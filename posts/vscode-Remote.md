---
title: vscode远程开发
data: 2019-10-11
tags: [vscode]
categories: [system]
---



vscode 远程编辑

1. 安装插件 remote-ssh

2. 配置.ssh/config 文件

```
Host 10.211.55.5     
HostName 10.211.55.5     
IdentityFile ~/.ssh/id_rsa     
User test 
```

3. 右侧显示显示器图标

4. 点击远程server 新建文件夹（connet to host in new window）

5. 保证 本地Git版本和远程server 版本一致，最好都是git2.0+