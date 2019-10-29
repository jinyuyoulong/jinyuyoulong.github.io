---
title: flutter安装
date: 2019-07-26
categories:
  - system
tages:
  - flutter
---



flutter安装

1.  git 下载 flutter：git clone -b stable https://github.com/flutter/flutter.git
2. 配置.zshrc 

```sh
export PATH=/Users/fanjinlong/dev/flutter/flutter/bin:$PATH
export ANDROID_HOME=/Users/fanjinlong/Library/Android/sdk
export PATH=${PATH}:${ANDROID_HOME}/tools
export PATH=${PATH}:${ANDROID_HOME}/platform-tools
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn	
# 记得配置完了，执行下 source ~/.zshrc 更新环境变量
```

3. 命令行执行 `flutter doctor` 检查环境配置情况。
4. 在 Android studio 中添加插件 flutter + dart
5. 根据`flutter doctor` 解决所有必要的问题
6. 运行 flutter run
7. 如果不能运行，查看报错，比如 `flutter emulators`——>`flutter emulators --launch Pixel_2_API_29`——> `flutter run`

```sh
Running "flutter pub get" in flutter_app...                         3.4s
Using hardware rendering with device Android SDK built for x86. If you get graphics artifacts, consider
enabling software rendering with "--enable-software-rendering".
Launching lib/main.dart on Android SDK built for x86 in debug mode...
Initializing gradle...
540.5s (!)
Resolving dependencies...
  634.0s (!)
Running Gradle task 'assembleDebug'...
Running Gradle task 'assembleDebug'... Done                       147.6s (!)
Built build/app/outputs/apk/debug/app-debug.apk.
Installing build/app/outputs/apk/app.apk...                         2.9s
D/EGL_emulation( 4282): eglMakeCurrent: 0xd681a0c0: ver 3 0 (tinfo 0xd680f300)
D/eglCodecCommon( 4282): setVertexArrayObject: set vao to 0 (0) 1 0
Syncing files to device Android SDK built for x86...
I/OpenGLRenderer( 4282): Davey! duration=788ms; Flags=1, IntendedVsync=1386986507632, Vsync=1386986507632, OldestInputEvent=9223372036854775807, NewestInputEvent=0, HandleInputStart=1386993436664, AnimationStart=1386993471165, PerformTraversalsStart=1386993474034, DrawStart=1387600641641, SyncQueued=1387601916409, SyncStart=1387607434150, IssueDrawCommandsStart=1387609441987, SwapBuffers=1387725240730, FrameCompleted=1387780735364, DequeueBufferDuration=31361000, QueueBufferDuration=260000,
I/Choreographer( 4282): Skipped 46 frames!  The application may be doing too much work on its main thread.     D/EGL_emulation( 4282): eglMakeCurrent: 0xd681a300: ver 3 0 (tinfo 0xd680f3d0)                                 D/eglCodecCommon( 4282): setVertexArrayObject: set vao to 0 (0) 1 0                                            Syncing files to device Android SDK built for x86...            183,943ms (!)
🔥  To hot reload changes while running, press "r". To hot restart (and rebuild state), press "R".
An Observatory debugger and profiler on Android SDK built for x86 is available at:
http://127.0.0.1:52933/6NColDWV2ps=/
For a more detailed help message, press "h". To detach, press "d"; to quit, press "q".

Initializing hot reload...
Reloaded 0 of 455 libraries in 956ms.
```

```sh
To run an emulator, run 'flutter emulators --launch <emulator id>'.
To create a new emulator, run 'flutter emulators --create [--name xyz]'	
```

