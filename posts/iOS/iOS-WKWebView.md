---
title: WKWebView
date: 2021-04-16
categories: [iOS]
tags: [iOS]
---
WKWebView是获取不到JSContext的，所以不能用JavaScriptCore进行交互。和js交互要用WKScriptMessageHandler协议方法 

//MARK: - WKNavigationDelegate 

//该代理提供的方法，可以用来追踪加载过程（页面开始加载、加载完成、加载失败）、决定是否执行跳转 

// 页面跳转的代理方法有三种，分为（收到跳转与决定是否跳转两种） 

// 剩下三个代理方法全都是与界面弹出提示框相关的 

// 针对于web界面的三种提示框（警告框、确认框、输入框）分别对应三种代理方法。 

//MARK: - WKScriptMessageHandler

//这个协议中包含一个必须实现的方法，这个方法是提高App与web端交互的关键，它可以直接将接收到的JS脚本转为OC或Swift对象。（当然，在UIWebView也可以通过“曲线救国”的方式与web进行交互，著名的Cordova框架就是这种机制

// 处理来自js的方法调用 

// 从web界面中接收到一个脚本时调用 js端的写法：

```javascript
// postMessage 参数不能为空，必须传点什么
// 格式为 window.webkit.messageHandlers..postMessage(null);
// 外部方法必须为 全局js方法
function scanClick() {
    window.webkit.messageHandlers.ScanAction.postMessage(null);
}
```
OC端的写法：

```objective-c

// 在某一个地方注册
[self.webView.configuration.userContentController addScriptMessageHandler:self name:@"ScanAction"];
// 在某一个地方移除
[self.webView.configuration.userContentController removeScriptMessageHandlerForName:@"ScanAction"];
//MARK: - WKScriptMessageHandler 代理方法的实现
- (void)userContentController:(WKUserContentController *)userContentController didReceiveScriptMessage:(WKScriptMessage *)message{
    if ([message.name isEqualToString:@"ScanAction"]) {
           NSLog(@"说吧，你想干点什么？");
       }
}
```
```objective-c
//
//  WKWebViewController.m
//  HTML_CSS_JS
//
//  Created by 范金龙 on 2020/4/28.
//  Copyright © 2020 FF. All rights reserved.
//
#import "WKWebViewController.h"
#import 
#import 
#import "WKDelegate.h"
@interface WKWebViewController ()
<
WKNavigationDelegate,
WKUIDelegate,
WKScriptMessageHandler
//WKDelegate
>
{
}
@property (nonatomic, strong)WKWebView *webView;
@end
@implementation WKWebViewController
static NSString *name = @"OCFunc";
// 避免循环引用，内存管理，这是一个经典的大环引用问题。
// 具体解决方案有好几种，比如：中间类，间接代理，提前手动删除打断。
// addScriptMessageHandler 会强引用self导致当前对象无法释放
- (void)viewWillAppear:(BOOL)animated{
    [super viewWillAppear:animated];
    [self.webView.configuration.userContentController addScriptMessageHandler:self name:@"toServer"];
    [self.webView.configuration.userContentController addScriptMessageHandler:self name:@"ScanAction"];
    [self.webView.configuration.userContentController addScriptMessageHandler:self name:name];
}
- (void)viewWillDisappear:(BOOL)animated{
    [super viewWillDisappear:animated];
    [self.webView.configuration.userContentController removeScriptMessageHandlerForName:@"toServer"];
    [self.webView.configuration.userContentController removeScriptMessageHandlerForName:@"ScanAction"];
    [self.webView.configuration.userContentController removeScriptMessageHandlerForName:name];
}
- (void)viewDidLoad {
    [super viewDidLoad];
    [self.view setBackgroundColor:[UIColor whiteColor]];
    // Do any additional setup after loading the view.
    [self initWKWebView];
}
- (void)initWKWebView
{
    WKWebViewConfiguration *configuration = [[WKWebViewConfiguration alloc] init];
    WKPreferences *preferences = [WKPreferences new];
    preferences.javaScriptCanOpenWindowsAutomatically = YES;
    preferences.minimumFontSize = 10.0;
    configuration.preferences = preferences;
    self.webView = [[WKWebView alloc] initWithFrame:self.view.frame configuration:configuration];
    NSString *urlStr = [[NSBundle mainBundle] pathForResource:@"wkDemo.html" ofType:nil];
    NSURL *fileURL = [NSURL fileURLWithPath:urlStr];
    [self.webView loadFileURL:fileURL allowingReadAccessToURL:fileURL];
    self.webView.UIDelegate = self;
    [self.view addSubview:self.webView];
}
//MARK: WKNavigationDelegate
//该代理提供的方法，可以用来追踪加载过程（页面开始加载、加载完成、加载失败）、决定是否执行跳转
// 页面开始加载时调用
- (void)webView:(WKWebView *)webView didStartProvisionalNavigation:(WKNavigation *)navigation{
}
// 当内容开始返回时调用
- (void)webView:(WKWebView *)webView didCommitNavigation:(WKNavigation *)navigation{
}
// 页面加载完成之后调用
- (void)webView:(WKWebView *)webView didFinishNavigation:(WKNavigation *)navigation{
    //向js注入关闭按钮事件监听
    NSString *script = @"document.querySelector('.close-btn').addEventListener('click',function() {window.webkit.messageHandlers.toServer.postMessage('close')},false)";
    [webView evaluateJavaScript:script completionHandler:^(id object, NSError * _Nullable error) {
        if(error){
            NSLog(@"evaluateJavaScript error : %@",error);
        }
    }];
}
// 页面加载失败时调用
- (void)webView:(WKWebView *)webView didFailProvisionalNavigation:(WKNavigation *)navigation{
}
// MARK:-
// 页面跳转的代理方法有三种，分为（收到跳转与决定是否跳转两种）
// 接收到服务器跳转请求之后调用
- (void)webView:(WKWebView *)webView didReceiveServerRedirectForProvisionalNavigation:(WKNavigation *)navigation{
}
// 在收到响应后，决定是否跳转
- (void)webView:(WKWebView *)webView decidePolicyForNavigationResponse:(WKNavigationResponse *)navigationResponse decisionHandler:(void (^)(WKNavigationResponsePolicy))decisionHandler{
    decisionHandler(WKNavigationResponsePolicyAllow);
}
// 在发送请求之前，决定是否跳转
- (void)webView:(WKWebView *)webView decidePolicyForNavigationAction:(nonnull WKNavigationAction *)navigationAction decisionHandler:(nonnull void (^)(WKNavigationActionPolicy))decisionHandler{
    decisionHandler(WKNavigationActionPolicyAllow);
}
//MARK: WKUIDelegate
// 创建一个新的WebView 待研究
- (WKWebView *)webView:(WKWebView *)webView createWebViewWithConfiguration:(WKWebViewConfiguration *)configuration forNavigationAction:(WKNavigationAction *)navigationAction windowFeatures:(WKWindowFeatures *)windowFeatures{
    return self.webView;
}
//MARK:- 剩下三个代理方法全都是与界面弹出提示框相关的
//针对于web界面的三种提示框（警告框、确认框、输入框）分别对应三种代理方法。下面只举了警告框的例子。
/**
 *  web界面中有弹出警告框时调用
 *
 *  @param webView           实现该代理的webview
 *  @param message           警告框中的内容
 *  @param frame             主窗口
 *  @param completionHandler 警告框消失调用
 */
- (void)webView:(WKWebView *)webView runJavaScriptAlertPanelWithMessage:(nonnull NSString *)message initiatedByFrame:(nonnull WKFrameInfo *)frame completionHandler:(nonnull void (^)(void))completionHandler
{
//    js 调用的alert方法，被wk拦截，在此处执行
    completionHandler();
}
- (void)webView:(WKWebView *)webView runJavaScriptConfirmPanelWithMessage:(NSString *)message initiatedByFrame:(WKFrameInfo *)frame completionHandler:(void (^)(BOOL))completionHandler{completionHandler(true);}
- (void)webView:(WKWebView *)webView runJavaScriptTextInputPanelWithPrompt:(NSString *)prompt defaultText:(NSString *)defaultText initiatedByFrame:(WKFrameInfo *)frame completionHandler:(void (^)(NSString * _Nullable))completionHandler{    completionHandler(@"输入");}
//MARK: WKScriptMessageHandler
//这个协议中包含一个必须实现的方法，这个方法是提高App与web端交互的关键，它可以直接将接收到的JS脚本转为OC或Swift对象。（当然，在UIWebView也可以通过“曲线救国”的方式与web进行交互，著名的Cordova框架就是这种机制
// 处理来自js的方法调用
// 从web界面中接收到一个脚本时调用
- (void)userContentController:(WKUserContentController *)userContentController didReceiveScriptMessage:(WKScriptMessage *)message{
    NSLog(@"%@",message.name);
    if ([message.name isEqualToString:@"ScanAction"]) {
           NSLog(@"扫一扫");
       }
    if ([message.name isEqualToString:@"OCFunc"]){//此处name为JS传出信息打包的标志
        //用message.body获得JS传出的参数体
        //handle coding..
        /*获得传出的字符串参数*/
        NSString * dataString = message.body;
        NSLog(@"wkwebview 获取js传出的数据%@",dataString);
        // 在需要调用JS的地方执行如下代码
        // 有参数
        [self.webView evaluateJavaScript:@"postInfo('参数1,参数2')"completionHandler:nil];
        // 无参数
        [self.webView evaluateJavaScript:@"postInfo()"completionHandler:nil];
        // 此处的 'postInfo()' 是前端的方法，需要前端告诉你
    }
}
- (void)dealloc
{
    NSLog(@"%s",__FUNCTION__);
}
@end

```
wkDemo.html 实例HTML的代码如下

```swift
            function scanClick() {
                window.webkit.messageHandlers.ScanAction.postMessage(null);
            }
            // <!-- 错误处理 -->
            window.onerror = function(err) {
                log('window.onerror: ' + err)
            }
            function log(message, data) {
                var log = document.getElementById('log')
                var el = document.createElement('p')
                el.className = 'logLine'
                el.innerHTML = "message: " + message +':<br/>' + (data ? ':<br/>' + JSON.stringify(data) : '')
                if (log.children.length) { log.insertBefore(el, log.children[0]) }
                else { log.appendChild(el) }
            }
            // function buttonOnClick = function (e) {} // 这种写法有问题,WKWebView 捕获的js方法必须为全局方法，也不可以是方法变量。
            // 下面这种形式正确
            function buttonOnClick(e) {
                window.webkit.messageHandlers.OCFunc.postMessage('close')//调用原生代码
            }
            function postInfo(name) {
                log(name)
            }

 
            html { font-family:Helvetica; color:#ddd; }
            h1 { color:steelblue; font-size:24pm; margin-top:24px; }
            button { margin:0 3px 10px; font-size:2pm; }
            .logLine { border-bottom:1px solid #ccc; padding:4px 2px; font-family:courier; font-size:11pm; }
            div{color: black;line-height:100%;border-color: #ccc; border-width:1px;}

        WebViewJavascriptBridge Demo
        
        buttons
            
            alert
            OC注入
            js 调用Native方法
        
        log
```