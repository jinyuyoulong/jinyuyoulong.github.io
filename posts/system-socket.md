---
title: Socket
author: fan
type: post
date: 2019-01-16T05:57:22+00:00
url: /socket/
categories:
  - 操作系统

---
<pre><code class="line-numbers">title: Socket
date: 2018-08-16
<<<<<<< HEAD:posts/2019-01-16-socket.md
tags: socket, HTTP
categories: HTTP
</code></pre>
=======
tags: [socket, HTTP]
categories: [HTTP]
```


>>>>>>> 9b93207d813e2b213031f967612e37c68194cf37:post/iOS-Scoket.md

iOS socket能做什么?
  
socket是TCP UDP IP HTTP 协议簇，封装为socket API
  
可以用来写 客户端，服务端模型，在两者之间进行数据交流
  
换句话说，socket API是用来进行数据交换的一簇协议，它包括TCP, UDP, IP, HTTP等协议。
  
那么socket在iOS中的应用场景有哪些呢？
  
蓝牙交互，WiFi传输，一般是将移动设备作为一个服务器来使用。
  
如果作为客户端使用，那就没什么可说的了，因为本来移动设备就是作为客户端的。