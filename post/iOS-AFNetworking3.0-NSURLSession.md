---
title: AFNetworking3.0/NSURLSession的优势
id: 351
categories:
  - iOS
date: 2016-03-15 10:53:52
tags:
---

很多时候，AFNetworking都是目前iOS开发者网络库中的不二选择。Github上2W+的star数足见其流行程度。而从iOS7.0开始，苹果推出了新的网络库继承者NSURLSession后，AFNetworking也毫不犹豫地加入了对其的支持。3.0+更加只是提供了NSURLSession的支持。
我们使用AFNetworking的时候，可能会有很多的朋友都会采用以下的写法：

AFHTTPSessionManager *sessionManager = [AFHTTPSessionManager manager];
sessionManager.requestSerializer     = [AFHTTPRequestSerializer serializer];
sessionManager.responseSerializer    = [AFHTTPResponseSerializer serializer];
[sessionManager GET:urlString
         parameters:parameters
           progress:progressBlock
            success:successHandler
            failure:failureHandler];

大概可以描述一下这个过程，每次开启一个网络请求时，首先新建一个AFHTTPSessionManager，然后将相关的requestSerializer和reponseSerializer赋值；最后发起相应的GET/POST等请求。
而如果是直接采用NSURLSession来请求网络呢，我们则经常会采用以下的写法：

NSURLSession *session =  [NSURLSession
sessionWithConfiguration:
[NSURLSessionConfiguration defaultSessionConfiguration]
 delegate:nil
  delegateQueue:[NSOperationQueue mainQueue]];

NSURLSessionDataTask *dataTask = [session dataTaskWithRequest:request
  completionHandler:completionHandler];

[dataTask resume];

这个过程其实和上面的基本一致。新建一个Session，然后新建task，激活task，完成网络请求。
那么现在问题来了。为什么每次都需要新建一个SessionManager/Session？如果在多个Task请求的情况下，如果采取一个共享的SessionManager/Session是否可行？如果可行，与之前每次新建SessionManager/Session相比，孰优孰劣？

本篇文章会告诉您：
1\. 为什么要使用NSURLSession而不是NSURLConnection
2\. 为什么要用共享的SessionManager/Session，而不是每次都启动一个新的

为什么要选择NSURLSession
NSURLSession在iOS7.0时被Apple提出后，虽然Apple一直对其良好的API设计大力推广，然而其能够达到的效果，似乎一直都和NSURLConnection不相伯仲。
特别是在网络的Dependecy依赖处理上，由于AFNetworking优秀的架构设计，NSURLSession甚至还不如NSURLConnection好用。那么，有什么理由切换到NSURLSession？ 2015年的WWDC似乎告诉了我们答案。
HTTP /2, 2015年5月RFC 7540正式发表的下一代HTTP协议，是1999年来HTTP 1.1发布后的首个更新。相对于前一个版本，HTTP /2以快著称。如下图，对相同图片、相同服务器的下载，在不同协议下所需的时间：

http2
这里我们并不打算展开HTTP /2的原理，有兴趣的同学可以Google之。根据2015的WWDC Session711，我们知道iOS9+，NSURLSession开始正式支持HTTP /2，也就意味着你的网络连接速度也可以有如上图那样的提升。
更人性化更优秀的API设计，HTTP /2的支持，这是否能成为你使用NSURLSession的理由？至少它们成为了说服我的理由。

为什么要尽量共享Session，而不是每次新建Session
在回答这个问题以前，我们先来聊聊网络的通讯协议。我们也都知道，HTTP协议是基于TCP协议的。所以在每次的HTTP请求之前，客户端和服务器端，都先需要经过TCP连接的三次握手，即每次请求之前，网络的数据都已经在客户端和服务器端之间来回了三次。如下图：

TCP三次握手（图片来源于网络)
事实上在HTTP 0.9, HTTP 1.0协议的时代，每次HTTP的请求，都需要先经过TCP的连接，然后才开始HTTP的请求，这样一个流程图，我们可以通过抓包看到：

抓包
那么，为了让我们的请求更快，避免每次都产生一个TCP三次握手，成了一个优化的选项。于是在HTTP 1.1中，出现了Connection: keep-alive这个选项。这个优化选项，可以使得客户端和服务器端复用一个TCP连接，从而减小每次的网络请求时间。

非共享Session

共享Session
聊到这里，本章提出的问题，其实答案已经逐渐明了了。没错，共享的Session将会复用TCP的连接，而每次都新建Session的操作将导致每次的网络请求都开启一个TCP的三次握手。
从上面两张图，我们可以清晰地看到，同样都是两次HTTP请求，共享Session的代码在第二次网络请求时少了TCP的三次握手的过程。即加速了整个网络的请求时间。
事实上，苹果的文档中，还对一个服务器最高的TCP并发有相应的描述：

HTTPMaximumConnectionsPerHost  Property
The maximum number of simultaneous connections to make to a given host.

Declaration
SWIFT
    var HTTPMaximumConnectionsPerHost: Int
OBJECTIVE-C
    @property NSInteger HTTPMaximumConnectionsPerHost
Discussion
This property determines the maximum number of simultaneous connections made to each host by tasks within sessions based on this configuration.

This limit is per session, so if you use multiple sessions, your app as a whole may exceed this limit. Additionally, depending on your connection to the Internet, a session may use a lower limit than the one you specify.

The default value is 6 in OS X, or 4 in iOS.

Availability
Available in iOS 7.0 and later.
我们可以看到，默认配置下，iOS对于同一个IP服务器的并发最大为4，OS X为6。而如果你没有使用共享的Session，则可能会超过这个数。
因此，如果能用共享的Session，还是用共享的吧。有些许的网络加速，也是一件不错的事情，您说呢？

本文来自 http://www.cocoachina.com/ios/20160202/15211.html 仅为收藏，方便查阅。