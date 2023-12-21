---
title: "Unity iOS 混合开发模式调研"
date: 2022-05-06T10:05:24+08:00
draft: false
toc: true
images:
categories:
  - Unity
tags: 
  - iOS
  - Unity
---
## Unity iOS 混合开发

unity+原生开发 有四种开发模式：
1. 以unity c#工程为主，由unity封装原生端的库为c# 第三方库，直接提供给unity工程，以plugin的方式使用。比如 iOS提供framework，安卓提供 aar
2. 以unity 导出的 原生工程为主。原生端在此基础上进行增量开发，原生端以原生第三方库的方式集成进导出工程。
3. 以原生工程为主。unity导出的工程可以编译成unity库。将此unity库集成进各端原生工程。比如：iOS 以unity.framework的方式引入使用 安卓引入 libunity.so。
4. 以原生工程为主，unity导出工程作为子工程依赖加入原生工程。此为第三种方式的变种。
5. 在4的基础上，unity window 和 native window 各自交互展示，此方案应用的场景为unity和原生的UI无任何重叠的现象
6. 在4的基础上, unity view 作为普通view加到 原生的view中，此方案应用的场景为有unity和原生UI重叠展示的情况

目前决定使用方案6，因为超级星球2.0UI改版后，业务重点大部分改到原生侧。由游戏化风格改为APP风格。

福清的Demo 工程是 flutter+unity的方式，本质是第四种。

混合开发代码示例如下：
```Objective-C
// unity plugin 导出的接口文件

// [!] important set UnityFramework in Target Membership for this file
// [!]           and set Public header visibility

#import <Foundation/Foundation.h>
// unity call 原生 的 接口
// NativeCallsProtocol defines protocol with methods you want to be called from managed
@protocol NativeCallsProtocol
@required
- (void) exitFromUnity;
- (void) getPhotos;
- (void)getUserWorkList:(char*)date;
- (Boolean) isSupportDevice;
- (void) callFromUnity;
// other methods
@end

__attribute__ ((visibility("default")))
@interface FrameworkLibAPI : NSObject
// 原生 call unity 的 接口 例如： [NSClassFromString(@"FrameworkLibAPI") reOpenCamera];
// call it any time after UnityFrameworkLoad to set object implementing NativeCallsProtocol methods
+(void) registerAPIforNativeCalls:(id<NativeCallsProtocol>) aApi;
+ (void)reOpenCamera;
+ (void)arDoor;
+ (void)arCamera;
+ (void)unitySendPhotoFilePath:(NSString *)fileStr;
+ (void)unitySendMonthWorkList:(NSString *)workStr;
+ (void)unitySendUserInfo:(NSString *)userInfo;
@end


// unity call 原生 的 接口 例：原生实现c方法
// 获取相册作品信息
- (void)getUserWorkList:(char *)date {
}
```
## unity call 原生
```cs
// cs代码
public class NativeAPI
{
	#if UNITY_IOS && !UNITY_EDITOR
    	[DllImport("__Internal")]
    	public static extern void OnUnityMessage(string message);
	#endif

    public static void SendMessageToFlutter(string message)
    {
	#if UNITY_ANDROID
        try
        {
            AndroidJavaClass jc = new AndroidJavaClass("com.xraph.plugin.flutter_unity_widget.UnityPlayerUtils");
            jc.CallStatic("onUnityMessage", message);
        }
        catch (Exception e)
        {
            Debug.Log(e.Message);
        }
	#elif UNITY_IOS && !UNITY_EDITOR
        OnUnityMessage(message);
	#endif
    }
}
// cs 使用
NativeAPI.SendMessageToFlutter(message);
```
```C++
// 原生工程 .mm 文件
// System.Void NativeAPI::OnUnityMessage(System.String)
IL2CPP_EXTERN_C IL2CPP_METHOD_ATTR void NativeAPI_OnUnityMessage_m1CF7151340955DF0256F5C6AD708DBE71F45AFB5 (String_t* ___message0, const RuntimeMethod* method)
{
	typedef void (DEFAULT_CALL *PInvokeFunc) (char*);

	// Marshaling of parameter '___message0' to native representation
	char* ____message0_marshaled = NULL;
	____message0_marshaled = il2cpp_codegen_marshal_string(___message0);

	// Native function invocation
	reinterpret_cast<PInvokeFunc>(OnUnityMessage)(____message0_marshaled);

	// Marshaling cleanup of parameter '___message0' native representation
	il2cpp_codegen_marshal_free(____message0_marshaled);
	____message0_marshaled = NULL;

}

```
```Objective-C
// unity IL2CPP 文件
extern "C" void ModulePlatformInfo_deviceLevelModel_m2113780681 ();
extern "C" void CrossPlatform_arCaptureFacePoint_m2135327796 ();
extern "C" void ModuleAudioMusical_parseMusicXML_m2975407064 ();

// file UnityAppController.mm
// Added by https://github.com/juicycleff/flutter-unity-view-widget
extern "C" void OnUnityMessage(const char* message)
{
    if (GetAppController().unityMessageHandler) {
        GetAppController().unityMessageHandler(message);
    }
}

// 原生 call unity
UnitySendMessage("CrossPlatform", "arCaptureFacePoint", data);


// flutter 和 unity交互的接口

// UnityAppController.h

// Added by https://github.com/juicycleff/flutter-unity-view-widget
typedef void(^unitySceneLoadedCallbackType)(const char* name, const int* buildIndex, const bool* isLoaded, const bool* IsValid);

typedef void(^unityMessageCallbackType)(const char* message);

// Added by https://github.com/juicycleff/flutter-unity-view-widget
@protocol UnityEventListener <NSObject>
- (void)onSceneLoaded:(NSString *)name buildIndex:(NSInteger *)bIndex loaded:(bool *)isLoaded valid:(bool *)IsValid;
- (void)onMessage:(NSString *)message;
```
#### unit call flutter

```Swift

1. 实现unity framework回调
controller = self.ufw?.appController()
controller?.unityMessageHandler = self.unityMessageHandlers
2. 通过回调方法，参数的字符串名称 进行分发原生方法调用
@objc
func unityMessageHandlers(_ message: UnsafePointer<Int8>?) {
    if let strMsg = message {
        globalChannel?.invokeMethod("events#onUnityMessage", arguments: String(utf8String: strMsg))
    } else {
        globalChannel?.invokeMethod("events#onUnityMessage", arguments: "")
    }
}
3. 通过channel 的字符串信息 进行 原生到flutter的方法调用分发
unity_page.dart
// Communication from Unity to Flutter
  void onUnityMessage(message) {
    print('Received message from unity: ${message.toString()}');
    print("================================================");

    var messageJson = json.decode(message);
    switch (messageJson['operate']) {
      case "openAlbum":
        openAlbum();
        break;
    }
@end
```
