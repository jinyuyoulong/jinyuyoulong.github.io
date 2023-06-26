---
title: "Moya http 请求 httpbody 无转义的json data数据，request的时候 会 自动添加转义符号"
date: 2023-02-16T11:46:27+08:00
draft: true
toc: true
images:
tags: 
  - iOS
---

Moya http 请求 httpbody 无转义的json data数据，request的时候 会 自动添加转义符号
```swift
struct YJJSONEncoding: ParameterEncoding {
    static let `default` = YJJSONEncoding()
    func encode(_ urlRequest: Alamofire.URLRequestConvertible, with parameters: Alamofire.Parameters?) throws -> URLRequest {
        var request = try urlRequest.asURLRequest()
        let data = try JSONSerialization.data(withJSONObject: parameters ?? [:], options: [.withoutEscapingSlashes])
        let json = String.init(data: data, encoding: .utf8)
        ffprint("httpbody \(json ?? "")")
        if request.value(forHTTPHeaderField: "Content-Type") == nil {
            request.setValue("application/json", forHTTPHeaderField: "Content-Type")
        }
        
        request.httpBody = data
        return request
    }
}

```
```sh
print httpbody {"content":"","contentType":2,"imageUrls":[{"height":1793,"url":"https://xxx.com/ios/content/image/7202302161142240.png","width":828}]}
```
服务端接收到的 数据：
```sh
requestHandyJson :{"topics":null,"place":"","contentData":{"imageUrls":[{"height":1793,"extendParam":null,"coverPicture":null,"width":828,"duration":null,"fileBytes":null,"url":"https:\/\/xxx.com\/ios\/content\/image\/7202302161142240.png"}],"extData":"","city":"","address":""},"like":0,"comment":0,"collection":null,"likeOrNot":2,"gmtCreate":"2023-02-16  11:42:25","share":null,"latitude":0,"authorAge":27,"authorSex":1,"friendState":0,"longitude":0,"contentType":2,"contentId":1045,"view":null,"vip":false,"authorNickName":"xx","authorId":7,"content":"","authorImage":"https:\/\/xxx.com\/7_1676368922.png"}
```