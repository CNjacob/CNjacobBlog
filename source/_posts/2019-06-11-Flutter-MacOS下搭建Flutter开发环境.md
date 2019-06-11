---
title: MacOS下搭建Flutter开发环境
date: 2019-06-11 11:22:05
tags: Flutter
---


## 1. 配置 Flutter 中国镜像
> 在搭建 Flutter 环境之前，因为众所周知的原因，有可能被墙，所以需要先为 Flutter 配置中国镜像。

###### 中国镜像地址
> 国内有两个镜像可以用，一个就是官方 Flutter 社区的国内镜像，另一个是上海交通大学 Linux 用户组的镜像，建议用官方 Flutter 社区的国内镜像。

* Flutter 社区
FLUTTER_STORAGE_BASE_URL: https://storage.flutter-io.cn
PUB_HOSTED_URL: https://pub.flutter-io.cn

* 上海交通大学 Linux 用户组
FLUTTER_STORAGE_BASE_URL: https://mirrors.sjtug.sjtu.edu.cn
PUB_HOSTED_URL: https://dart-pub.mirrors.sjtug.sjtu.edu.cn

<!--more-->

###### 配置方法
> 需要设置两个环境变量：PUB_HOSTED_URL 和 FLUTTER_STORAGE_BASE_URL。

在 ~/.bash_profile 里添加：

```shell
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```

保存文件后，再运行

```shell
source ~/.bash_profile
```

## 2. 安装 Android 开发环境
> 为了 Flutter 可以编译成 Android APK，和运行在 Android 模拟器上，需要搭建 Android 开发环境。安装 Android Studio，安装成功后，会自带 Android SDK。Androdi Studio 的下载地址有三个，选一个可以下载的地址：

* [官方地址](developer.android.com/studio)
* [官方中文地址](developer.android.google.cn/studio/)
* [国内第三方地址](www.androiddevtools.cn/)

###### 配置 Android SDK 环境变量
打开 Android Studio，选择 Confiure -> 'SDK Manager'：
![](image_01.png)
在打开的窗口中就能看到 Android SDK 的路径:
![](image_02.png)
在 ~/.bash_profile 里添加：

```shell
export ANDROID_HOME=/Users/****/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```

保存文件后，再运行

```shell
source ~/.bash_profile
```

###### 创建 Android 模拟器
打开 Android Studio，选择 Confiure -> 'AVD Manager'：
![](image_03.png)
在打开的页面里点击 Create Virtual Device...：
![](image_04.png)
在 Phone 里选择一个设备，这里选择 Pixel 2 XL：
![](image_05.png)
然后一直点击 Next，就成功创建了 Android 模拟器。

## 3. 安装 iOS 开发环境
> 为了 Flutter 可以编译成 iOS 安装包，和运行在 iOS 模拟器上，需要搭建 iOS 开发环境。
直接安装Xcode即可

## 4. Flutter SDK

###### 下载 Flutter SDK
1. 你可以在 [Flutter SDK](https://flutter.dev/docs/development/tools/sdk/releases?tab=macos) 的下载页面，选择你想要的版本，一般选择稳定版的，最新的稳定版是 v1.5.4-hotfix.2。
2. 选一个路径来存放 Flutter SDK ，例如 /Users/jacob/sdk， 在这个位置下解压缩 Flutter SDK 的 zip 包：

```shell
cd /Users/jacob/sdk
unzip ~/Downloads/flutter_macos_v1.0.0-stable.zip
```

###### 设置 Flutter SDK 的环境变量

在 ~/.bash_profile 里添加：

```shell
export FLUTTER_HOME=/Users/jacob/sdk
export PATH=$PATH:$FLUTTER_HOME/bin
```

保存文件后，再运行

```shell
source ~/.bash_profile
```

###### 运行 flutter doctor
> 为了验证 Flutter 是否安装成功，运行：

```shell
flutter doctor
```

看到输出如下的结果：

```shell
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, v1.5.4-hotfix.2, on Mac OS X 10.14.4 18E226, locale
    zh-Hans-CN)
 
[!] Android toolchain - develop for Android devices (Android SDK version 28.0.3)
    ! Some Android licenses not accepted.  To resolve this, run: flutter doctor
      --android-licenses
[!] iOS toolchain - develop for iOS devices (Xcode 10.2)
    ✗ libimobiledevice and ideviceinstaller are not installed. To install with
      Brew, run:
        brew update
        brew install --HEAD usbmuxd
        brew link usbmuxd
        brew install --HEAD libimobiledevice
        brew install ideviceinstaller
    ✗ ios-deploy not installed. To install:
        brew install ios-deploy
[!] Android Studio (version 3.3)
    ✗ Flutter plugin not installed; this adds Flutter specific functionality.
    ✗ Dart plugin not installed; this adds Dart specific functionality.
[!] VS Code (version 1.35.0)
    ✗ Flutter extension not installed; install from
      https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter
[!] Connected device
    ! No devices available

! Doctor found issues in 5 categories.
```

说明，Flutter SDK 已经安装成功。但是也可以看到 flutter 的报错，请按照报错的提示修复，例如：

1. Android toolchain - develop for Android devices（Android证书的问题）
    运行脚本修复即可

    ```shell
    flutter doctor --android-licenses
    ```

2. iOS toolchain - develop for iOS devices（iOS的问题）

```shell
[!] iOS toolchain - develop for iOS devices (Xcode 10.2)
    ✗ libimobiledevice and ideviceinstaller are not installed. To install with
      Brew, run:
        brew update
        brew install --HEAD usbmuxd
        brew link usbmuxd
        brew install --HEAD libimobiledevice
        brew install ideviceinstaller
    ✗ ios-deploy not installed. To install:
        brew install ios-deploy
```
这里列出了出现的问题，并且给出了解决方案，需要你按照提示运行相应的命令

3. Android Studio

```shell
[!] Android Studio (version 3.3)
    ✗ Flutter plugin not installed; this adds Flutter specific functionality.
    ✗ Dart plugin not installed; this adds Dart specific functionality.
```

`Android Studio`未下载`Flutter`和`Dart`插件。
打开`Android Studio`，选择`Confiure -> 'Plugins'`：
![](image_06.png)
然后搜索下载Flutter和Dart

4. VS Code

```shell
[!] VS Code (version 1.35.0)
    ✗ Flutter extension not installed; install from
      https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter
```

VS Code未下载Flutter环境
打开`VS Code`搜索下载`Flutter`即可
![](image_07.png)

5. Connected device

```shell
[!] Connected device
    ! No devices available
```
启动一下`Xcode`中的模拟器即可

## 5. Flutter IDE
###### Android Studio
> 我们知道`Android Studio`是用来开发`Android`的，但是也可以开发`Flutter`。
> 前面的步骤中已经安装了`Android Studio`，并且已下载相关插件`Flutter`和`Dart`，

打开`Android Studio`后，可以看到`Start a new Flutter project`
![](image_08.png)

###### VS Code
> VS Code 是一个轻量级编辑器，支持 Flutter 的开发。

1. 安装[VS Code](https://code.visualstudio.com) 最新稳定版

2. 安装`Flutter`插件
    * 打开`VS Code`。
    * 快捷键`Shift+cmd+P(MacOS)`打开命令面板
    * 输入`install`, 选择`Extensions: Install Extensions`，如下图：
    
    ![](image_09.png)
    
    * 在`Extensions`的搜索框里输入`Flutter`,如下图：
    
    ![](image_10.png)
    
    * 选择`Flutter`并点击`Install`，我这边已经下载过了，所以是`Uninstall`
    * 安装完后，重启`VS Code`
    * 快捷键`Shift+cmd+P(MacOS)`打开命令面板，输入`Flutter`，如果看到如下图的`Flutter`命令，说明安装成功
    
    ![](image_11.png)


