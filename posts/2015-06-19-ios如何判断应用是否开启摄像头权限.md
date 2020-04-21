---
title: iOS如何判断应用是否开启摄像头权限
author: fan
type: post
date: 2015-06-19T03:25:28+00:00
url: /ios如何判断应用是否开启摄像头权限/
duoshuo_thread_id:
  - 6278603270403392258
  - 6278603270403392258
categories:
  - iOS

---
<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  <span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">NSString</span> * mediaType = <span style="font-variant-ligatures: no-common-ligatures; color: #723eae">AVMediaTypeVideo</span>;
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; <span style="font-variant-ligatures: no-common-ligatures; color: #723eae">AVAuthorizationStatus</span>&nbsp; authorizationStatus = [<span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">AVCaptureDevice</span> <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">authorizationStatusForMediaType</span>:mediaType];
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; <span style="font-variant-ligatures: no-common-ligatures; color: #063698">if</span> (authorizationStatus == <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">AVAuthorizationStatusRestricted</span> || authorizationStatus == <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">AVAuthorizationStatusDenied</span>) {
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(87, 44, 179);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; &nbsp; &nbsp; </span><span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">UIAlertController</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> * alertC = [</span><span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">UIAlertController</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>alertControllerWithTitle<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #c3c300">@"</span><span style="font-family: &#39;Heiti SC Light&#39;; color: rgb(195, 195, 0);">摄像头访问受限</span><span style="font-variant-ligatures: no-common-ligatures; color: #c3c300">"</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>message<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">nil</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>preferredStyle<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span>UIAlertControllerStyleAlert<span style="font-variant-ligatures: no-common-ligatures; color: #000000">];</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(87, 44, 179);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; &nbsp; &nbsp; [</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">self</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>presentViewController<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:alertC </span>animated<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">YES</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>completion<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">nil</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">];</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(87, 44, 179);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; &nbsp; &nbsp; </span><span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">UIAlertAction</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> * action = [</span><span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">UIAlertAction</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>actionWithTitle<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #c3c300">@"</span><span style="font-family: &#39;Heiti SC Light&#39;; color: rgb(195, 195, 0);">取消</span><span style="font-variant-ligatures: no-common-ligatures; color: #c3c300">"</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>style<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span>UIAlertActionStyleCancel<span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>handler<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:^(</span><span style="font-variant-ligatures: no-common-ligatures; color: #b9860a">UIAlertAction</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> *action) {</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo; color: rgb(87, 44, 179);">
  <span style="font-variant-ligatures: no-common-ligatures; color: #000000">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; [</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">self</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>dismissViewControllerAnimated<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">YES</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000"> </span>completion<span style="font-variant-ligatures: no-common-ligatures; color: #000000">:</span><span style="font-variant-ligatures: no-common-ligatures; color: #063698">nil</span><span style="font-variant-ligatures: no-common-ligatures; color: #000000">];</span>
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; &nbsp; &nbsp; }];
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; &nbsp; &nbsp; [alertC <span style="font-variant-ligatures: no-common-ligatures; color: #572cb3">addAction</span>:action];
</p>

<p style="margin-top: 0px; margin-bottom: 0px; font-family: Menlo;">
  &nbsp; &nbsp; }<span style="font-variant-ligatures: no-common-ligatures; color: #063698">else</span>{
</p>

}