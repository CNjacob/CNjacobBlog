---
title: Cocoapods安装及使用
date: 2019-03-27 16:18:52
tags: iOS
author: "CNjacob"
---

## 1.CocoaPods简介
> CocoaPods是负责管理iOS或MacOS项目的第三方框架。
> CocoaPods的项目源码在Github上管理。项目从2011年8月12日开始,CocoaPods的出现使得我们可以节省设置和更新第三方开源库的时间。

<!--more-->

## 2.CocoaPods安装
1.安装需要用到Ruby，虽然Mac自带了Ruby，不过版本有点老了，最好更新一下
```shell
sudo gem update --system
```
接下来输入系统密码就可以安装了，输入密码时不会显示的，输完回车就行了

2.因为Ruby的软件源rubygems.org被屏蔽了，所以要更换源
```shell
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
```

3.接下来查看下源路径是否更换了
```shell
gem sources -l
```

4.接下来安装Cocoapods
```shell
sudo gem install cocoapods
```

5.安装完后,查看是否成功以及当前CocoaPods的版本
```shell
pod --version
```

## 2.CocoaPods使用
1.Xcode 创建 CocoapodsTest项目
![](createXcodeProject.png)

2.通过终端命令cd到项目根目录下，使用 pod init 命令初始化pod项目
```shell
cd /Users/jacob/Desktop/CocoapodsTest
pod init
```

3.编辑Podfile文件
```shell
vim Podfile
```

4.在target下导入AFNetworking，导入代码如下
```shell
pod 'AFNetworking', '~> 3.2.1'
```
![](vimPodfile.png)

5.执行 pod install 命令加载 AFNetworking
```shell
pod install
```
![](podInstall.png)
执行完成后，会增加 CocoapodsTest.xcworkspace 、 Podfile.lock 文件和 Pods 文件夹，其中加载的第三方库在 Pods 文件夹中
![](openProject.png)

6.通过 CocoapodsTest.xcworkspace 打开项目
![](showProject.png)

