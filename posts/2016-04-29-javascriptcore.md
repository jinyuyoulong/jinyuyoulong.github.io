---
title: JavaScriptCore
author: fan
type: post
date: 2016-04-29T09:43:54+00:00
url: /javascriptcore/
duoshuo_thread_id:
  - 6278911626179511042
  - 6278911626179511042
categories:
  - iOS
tags:
  - javascriptCore

---
JavaScript 和OC原生交互

    <br />- (void)ocCallJSFunction{
    JSContext context = [[JSContext alloc]init];
    JSValue jsValue = [context evaluateScript:@"21+7"];
    int iVal = [jsValue toInt32];
    NSLog(@"js value=%@,int=%d",jsValue, iVal);
    [context evaluateScript:@"var arr = [21, 7, 'fanyiqing.com'];"];
    JSValue jsArr = context[@"arr"];
    NSLog(@"JS Array:%@ length:%@",jsArr,jsArr[@"length"]);
    jsArr[1] = @"blog";
    jsArr[7] = @7;
    NSLog(@"JS Array:%@, length:%d",jsArr,[jsArr[@"length"] toInt32]);
    NSArray nsarray = [jsArr toArray];
    NSLog(@"nsarray:%@",nsarray);
    }