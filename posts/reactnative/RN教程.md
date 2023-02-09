---
title: "RN教程"
date: 2021-05-24T20:43:22+08:00
toc: true
images:
tags: 
  - ReactNative
---
[TOC]

## 搭建开发环境

安装依赖
iOS
必须安装的依赖有：Node、Watchman、Xcode 和 CocoaPods。
安卓
必须安装的依赖有：Node、Watchman、JDK 和 Android Studio。

最佳实践：使用以下方式创建新项目

create-react-native-app demo0 设置创建项目的可选项
启动
```
- yarn android
- yarn ios
- yarn web
```

接口环境配置：

使用青花瓷抓包工具

配置：Proxy-》Mac OS proxy  监听本机代理

tools-> map remote 设置允许，添加远程端口映射,或者 map local做本地文件映射

配置测试机 的IP代理



## 创建项目
```
npx react-native init AwesomeProject
或
create-react-native-app demoName
这种方式创建的项目有iOS Android web 三端 最佳实践
```
## 编译并运行 React Native 应用
```
yarn ios # 或者 yarn react-native run-ios
yarn android
yarn web
```

## reload

iOS： cmd+r

安卓: cmd+m

```
brew install node
brew install watchman
# 使用nrm工具切换淘宝源
npx nrm use taobao
npm install -g yarn// Yarn是 Facebook 提供的替代 npm 的工具，可以加速 node 模块的下载。
brew install cocoapods

---
npm install -g expo-cli
npm install -g create-react-native-app 

```

验证 metro 是否启动 访问https://127.0.0.1:8081 可以正常响应

### 矢量图使用

引入node包

yarn add react-native-vector-icons

将react-native-vector-icons/Fonts 引入xcode

修改info.plist 加入字体包

```
<key>UIAppFonts</key>
    <array>
      <string>Entypo.ttf</string>
      <string>EvilIcons.ttf</string>
      <string>FontAwesome.ttf</string>
      <string>Foundation.ttf</string>
      <string>Ionicons.ttf</string>
      <string>MaterialIcons.ttf</string>
      <string>Octicons.ttf</string>
      <string>SimpleLineIcons.ttf</string>
      <string>Zocial.ttf</string>
      <string>MaterialCommunityIcons.ttf</string>
    </array>
```

pod update

file-> workspace setting->legacy build system

build setting->library search paths-> CocoaAsyncSocket->修改寻找方式recursive

修改pod包bug 

React Navigation 4 API

```
const MineStack = createStackNavigator({
  Mine: MineScreen,
  Detail: DetailsScreen,
  Setting: SettingSrceen
});
```

## 安卓开发

api请求失败是因为本地通过localhost访问，iOS模拟器正常，安卓模拟器异常。

需要改为通过本机ip访问在header中添加host字段

```js
 var url = 'http://192.168.0.5/index.php/api/index';
fetch(url, {
        method: 'GET',
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json;charset=utf-8', //数据格式 json或者key-value形式
            "Connection": "close",
            'Host': '000.com',
        },
    })
```

"Connection": "close",iOS为close 安卓默认为 keep-alive

请求的服务器地址是本地的环境的不行，必须线上才可以，这是android问题，ios正常

最后解决的方法是用安卓手机usb调试，然后没有连wifi连的是自己的4g网络，就不报这样的错误了，接口用的是线上的http，没有用https，用的是fetch传formData的数据，

## bind

this.back.bind(this)，我back就是一个方法为啥还要再bind(this). 其实就是一个作用域，绑定这个作用域中的方法。

那么其实我们有两种写法去定义onPress的响应方法。
1.不加bind（this）

```
onPress={this.back}
....
  back = () => {
        const {navigator} = this.props;
        navigator.pop();
    }

```

这种写法不用去bind了，

()=>{} 这种形式的代码，语法规定就是(function(){}).bind(this),即自动添加了bind this

2.需要加bind

```
onPress={this.back.bind(this)}

....

  back() {
        const {navigator} = this.props;
        navigator.pop();
    }

```

## web和RN交互，数据传递

### 将RN变量传入Web

webview 使用的库是 react-native-webview ，在RN 0.60之前 通过onMessage方法传递交互，具体不细讲。因为已经过时了。0.60之后 官方发现还是直接插入js代码更好用injectedJavaScript，所以最佳实践是这样的：

```react
// class中
// 注入一个方法并绑定给 window.launchScan 以备 RN 调用
    getInjectedJS = () => {
        const token = this.state.token;
        const projectId = '456';
        return `
                window.token = '${token}';// 用window将token声明成全局
                token2 = '${token}'; 
                window.projectId = '${projectId}';
                function btnClick(){
                  alert(window.token)
                }
                `
    }
<WebView
    style={{ width: width, height: height }}
    source = {{uri: this.state.url}}
    onLoadProgress={({nativeEvent}) => this.setState(
      {progress: nativeEvent.progress}
    )}
    bounces={false}
    allowFileAccess={true}//是否允许访问系统文件
    javaScriptEnabled
    ref={(webView) => {this.webView = webView}}
    domStorageEnabled={false}
    onMessage={this.onMessage.bind(this)}
    injectedJavaScript={this.getInjectedJS()} // ** 注意：这里是重点 **

    // onLoad={this.webViewload.bind(this)}
    onLoadEnd={this.onLoadEnd.bind(this)}
    onError={this.onError}
    renderError={this.renderError}
    onNavigationStateChange={this.onNavigationStateChange.bind(this)}
/>
```

js 字符串将会插入到web的scripts标签中，当做正常的js代码执行。

## 打包

### iOS

```
先创建ios/bundle目录
npx react-native bundle --entry-file index.js --platform ios --dev false --bundle-output ios/bundle/index.ios.bundle --assets-dest ios/bundle
```

注销application中的debug条件代码

将资源文件assets+ios.bundle加到项目中，直接可以编译通过的话就可以打包了

node编译报错

解决：build phases->buildle rn image
使用了非标准的 nodejs 安装流程

```
如果你使用了非标准的 nodejs 安装流程，
在Xcode中选择Project -> Build Phases -> Bundle React Native code and images，
把NODE_BINARY改为node可执行文件的绝对路径
你可以在终端命令行中执行 `$ which node` 来查看你当前node的绝对路径
export NODE_BINARY=/Users/fanjinlong/.nvm/versions/node/v12.9.0/bin/node
../node_modules/react-native/scripts/react-native-xcode.sh

```

打包失败

yarn start --reset-cache

### Android

1. 生成index.android.bundle 文件在src/main/assets/目录下

2. 修改配置: 编译平台，去除debug代码，添加权限配置等

3. 生成签名，编译release包： build -> genero signed build apk
4. as编译打包，或命令行打包





```sh
也可以as生成，下面是命令行生成
keytool -genkey -alias my-release-key.keystore -keyalg RSA -validity 20000 -keystore my-release-key.keystore

// release.keystore 签名需要放到 android/app/build/ ，可以不放，使用Androidstudio 打包时指定文件路径就行

查看keystore 信息
keytool -v -list -keystore my-release-key.keystore
```

#### 安卓打包改配置

APP displayName：android/app/src/main/res/values/strings.xml app_name

APP logo: res/mipmap rpx命令编译失败，不能用

增加签名证书，修改 android/app/gradle.properties

```
# Version of flipper SDK to use with React Native
FLIPPER_VERSION=0.33.1
# 新加:
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=com.suipingbang.www
MYAPP_RELEASE_STORE_PASSWORD=111111
MYAPP_RELEASE_KEY_PASSWORD=111111
```

修改android/app/build.gradle(app)

```
android{
...
  signingConfigs {
      release {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
}
```

更改`build.gradle` 文件中的 `applicationId` 属性 应用ID

rn命令行编译js代码->bundle资源束，有js map和没有，在项目目录下。

```
npx react-native bundle --platform android --dev false --reset-cache --entry-file index.js --bundle-output ./android/app/build/generated/assets/react/release/index.android.bundle --assets-dest android/app/build/generated/res/react/release --sourcemap-output android/app/build/generated/sourcemaps/react/release/index.android.bundle.map
```

```
npx react-native bundle --platform android --dev false --reset-cache --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
```

bundle可能会导出失败，由于没有目录，所以需要在android/app/src/main目录下创建assets目录
def enableSeparateBuildPerCPUArchitecture = true 设置为true根据CPU生成不通的apk包

#### 打包 apk（在android/app/build/outputs/apk 生成app-release.apk）

```sh
cd android 
./gradlew clean && ./gradlew assembleRelease 该打包方式遇到问题,后来也成功了

在设备上安装release版本
npx react-native run-android --variant=release 这个成功

AndroidStudio 打包
build/Generate Signed Bundle or APK -> APK -> 配置keystores -> 选择release， V1 V2两个都要勾选
```

 `app ->release->app-release.apk` --> android studio 打包apk发布包 文件存放路径：

`app/build/outputs/apk/release/app-release.apk` --> npx命令行输出目录：



Metro js 打包热更新,用于开发，起下发js代码的server，编译打包时坑了我。apk闪退。

如果是 react-native 0.6+ 每次 yarn / npm install 之后需要先运行 `npx jetify`检查一遍。



使用AS4 IDE打包release 不行，启动直接崩溃。只能使用npx。两者的apk输出目录不是同一个地方！

参考https://juejin.im/post/5dc8c080f265da4cf022ddc6

###  React Native 相关的 Activity 和 Application

创建一个继承自 `com.facebook.react.ReactActivity` 的 Activity

**重写 `getMainComponentName()` 方法，返回的字符串必须和前面的 `AppRegistry.registerComponent('navigation', () => App)` 里的 `navigation` 对应，表示该 Activity 会显示对应组件里的内容。**

### Android

编辑 `android/app/src/main/res/values/strings.xml` 文件：

### iOS

编辑 `ios/test/Info.plist` 文件：



##### Android启动图标更换后部分手机未生效解决办法

1、方法一：clean项目，下载应用，重新手机，重新安装
2、方法二：修改手机主题（马上生效，但是VIVO手机出现再次切换原主题恢复原图标问题）
3、方法三：重命名启动图标名称，重新运行安装项目即可（最佳方案）
4、方法四：更改应用版本号

可能原因：手机上有缓存，不是app内部缓存，而是launcher缓存。

### 上架

软著如何统计代码行数？

```shell
# 统计当前目录下的 app 文件夹中，所有 JS 文件的代码行数
find ./app "(" -name "*.js" ")" -print | xargs wc -l
# 统计当前目录下的 ios 文件夹中，所有 Objective-C 的代码行数
find ./ios "(" -name "*.h" -or -name "*.m" ")" -print | xargs wc -l
#统计当前目录下的 android 文件夹中，所有 Java 的代码行数
find ./android "(" -name "*.java" ")" -print | xargs wc -l
```

