---
toc: true
title: 使用cocoapods创建属于自己的公有库或私有库
date: 2019-03-27 16:19:16
tags: iOS
author: "CNjacob"
---

> 最近总结了一下如何使用cocoapods管理自己的Pod库，文章简要说明了如何使用cocoapods创建属于自己的公有库或私有库。写得比较匆忙，有错的地方还请指正，我会及时修改

<!--more-->

## 1. 如何创建共有库

### 1.1 注册Trunk

##### 1.1.1 版本要求
> trunk需要CocoaPods 0.33版本以上，用 pod --version 命令查看版本
```shell
pod --version
```
> 我的CocoaPods是 1.6.0 版本
![](/podVersion.png)

> 如果版本低，需要升级
```shell
sudo gen install cocoapods
pod setup
```

##### 1.1.2 开始注册
> 15375187600@163.com 代表你的邮箱
> 'CNjacob' 代表你的用户名
> --description='macbook pro' 描述性文字
> --verbose可以输出详细debug信息，方便出错时查看
```shell
pod trunk register 15375187600@163.com 'CNjacob' --description='macbook pro' --verbose
```

##### 1.1.3 查看注册信息
> 通过 pod trunk me 命令查看自己是否注册过Trunk
```shell
pod trunk me
```
> 我这里是已经注册过了的，其中包含你的name、email、since、Pods、sessions，Pods为你往CocoaPods提交的所有的Pod
![](/trunkMe.png)

##### 1.1.4 给项目添加其他维护者
> JacobBluetoothKit 为Pod项目名称
> mark.gu@163.com 为维护者邮箱
```shell
pod trunk add-owner JacobBluetoothKit mark.gu@163.com
```

### 1.2 创建自己的Pod

##### 1.2.1 创建Pod
> 使用 pod lib create 引导过程来创建整个pod
```shell
pod lib create CNjacobBleManagerKit
```

>进入引导过程
![](/libCreate.png)

> 整个引导过程有6步选择，如下图:
![](/createLibGuide.png)


> 1.选择系统版本，iOS / macOS
```shell
What platform do you want to use?? [ iOS / macOS ]
 > iOS
 ```

> 2.选择语言，[ Swift / ObjC ]
```shell
What language do you want to use?? [ Swift / ObjC ]
 > ObjC
```

> 3.制作演示应用程序，[ Yes / No ]
```shell
Would you like to include a demo application with your library? [ Yes / No ]
 > Yes
```

> 4.选择测试框架，[ Specta / Kiwi / None ]
```shell
Which testing frameworks will you use? [ Specta / Kiwi / None ]
 > Kiwi
```

> 5.基于视图的测试，[ Yes / No ]
```shell
Would you like to do view based testing? [ Yes / No ]
 > No
```

> 6.类的前缀
```shell
What is your class prefix?
 > CNjacob
```

> 创建完成后会自动打开Xcode工程
![](/createSuccess.png)

##### 1.2.2 .podspec 文件配置
> 可以通过 CNjacobBleManagerKit.podspec 文件来配置工程
![](/settingPodspec.png)

> 讲一下各项配置的含义
```
s.name                  名称，pod search 搜索的关键词,注意这里一定要和.podspec的名称一样,否则报错
s.version               版本号
s.summary               简介

s.description           详细介绍

s.homepage              项目主页地址
s.license               许可证
s.author                作者
s.source                项目的地址
s.social_media_url      社交网址

s.ios.deployment_target 支持的pod最低版本

s.source_files          需要包含的源文件

s.resource_bundles      资源文件（图片等）
// 其他

s.public_header_files   公开的头文件
s.resources             资源文件
s.dependency            依赖库，不能依赖未发布的库，可以写多个依赖库
```

##### 1.2.3 代码提交
> 完成.podspec 文件配置后，需将代码提交至GitHub，并打上tag，tag必须与.podspec 文件配置中的版本号一致
![](/commitAndTag.png)

> 代码提交完成
![](/commitSuccess.png)

##### 1.2.4 部署库
> 1.检查Podspec是否正确
```shell
pod lib lint
pod spec lint
```

> pod lib lint 和 pod spec lint。它们之间的区别在于pod lib lint不访问网络，而是pod spec lint检查外部仓库和相关标签
![](/podLint.png)

> 2.发布
```shell
pod trunk push CNjacobBleManagerKit.podspec
```

> 如下所示，发布成功
![](/trunkPushSuccess.png)

> 验证仓库
```shell
pod search CNjacobBleManagerKit
```

> 可能会出错，如下所示
![](/searchFailed.png)

> 解决办法，删除缓存，重新 pod setup ，需要等待一段时间
![](/deleteCacheAndSetup.png)

> 再次验证仓库，可以看到已经发布成功
![](/searchSuccess.png)


## 2. 如何创建私有库

### 2.1 创建私有仓库Specs
> 如果想利用pod安装私有库，那么就得创建和cocoapods官方一样的结构，我们想来看看cocoapods官方的结构，cocoapods所有公共库文件都存放在CocoaPods spec远端文件地址，如果在电脑上安装了cocoapods它会从这个地址clone一份到本地，每次pod update 都会更新这个本地仓库，首先先创建一个私有的库
![](/createRepository.png)

> 在终端执行
```shell
pod repo add CNjacobSpecs https://github.com/CNjacob/CNjacobSpecs.git
```

> 然后执行
```shell
open ~/.cocoapods/repos
```
> 会开看到在repos中创建了一个私有的仓库 CNjacobSpecs ， master 是cocoapods官方的
![](/repos.png)

### 2.2 向私有的 spec repo 里添加 podspec文件
> 1.在1.2中创建了属于自己的Pod，接下来在GitHub上将其修改为私有库
![](/privatePod.png)

> 2.通过终端命令 cd 到Pod项目的根目录下，向 CNjacobSpecs 里添加 CNjacobBleManagerKit.podspec 文件
```shell
cd /Users/jacob/Desktop/Cocoapods/CNjacobBleManagerKit
pod repo push CNjacobSpecs CNjacobBleManagerKit.podspec
```
> 3.命令执行结束，可看到 repos/CNjacobSpecs 目录下增加了一个 CNjacobBleManagerKit 文件夹，表示添加成功了
![](/pushToCNjacobSpecsSuccess.png)
