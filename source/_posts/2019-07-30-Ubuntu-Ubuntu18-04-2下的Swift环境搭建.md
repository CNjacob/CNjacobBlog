---
title: Ubuntu18.04.2下的Swift环境搭建
date: 2019-07-30 10:17:30
tags: Ubuntu
---

> 搭建环境 Ubuntu18.04.2 + swift5.0.2

<!--more-->

## 1.安装所需的依赖项

```shell
apt-get update
apt-get install clang libicu-dev
```

## 2.下载对应ubuntu的版本和对应的数字签名

```shell
mkdir Swift
cd Swift
wget https://swift.org/builds/swift-5.0.2-release/ubuntu1804/swift-5.0.2-RELEASE/swift-5.0.2-RELEASE-ubuntu18.04.tar.gz
wget https://swift.org/builds/swift-5.0.2-release/ubuntu1804/swift-5.0.2-RELEASE/swift-5.0.2-RELEASE-ubuntu18.04.tar.gz.sig
```

## 3.将PGP密钥导入密钥环

```shell
wget -q -O - https://swift.org/keys/all-keys.asc | \
  gpg --import -
```

> 可看到控制台信息如下

```shell
gpg: keybox '/root/.gnupg/pubring.kbx' created
gpg: /root/.gnupg/trustdb.gpg: trustdb created
gpg: key D441C977412B37AD: public key "Swift Automatic Signing Key #1 <swift-infrastructure@swift.org>" imported
gpg: key 9F597F4D21A56D5F: public key "Swift 2.2 Release Signing Key <swift-infrastructure@swift.org>" imported
gpg: key 63BC1CFE91D306C6: public key "Swift 3.x Release Signing Key <swift-infrastructure@swift.org>" imported
gpg: key EF5430F071E1B235: public key "Swift 4.x Release Signing Key <swift-infrastructure@swift.org>" imported
gpg: key 7638F1FB2B2B08C4: public key "Swift Automatic Signing Key #2 <swift-infrastructure@swift.org>" imported
gpg: key 925CC1CCED3D1561: public key "Swift 5.x Release Signing Key <swift-infrastructure@swift.org>" imported
gpg: Total number processed: 6
gpg:               imported: 6
```

## 4.解压下载的swift

```shell
tar xzf swift-5.0.2-RELEASE-ubuntu18.04.tar.gz
```

## 5.环境变量配置

```shell
vi /etc/profile
```

> i进入编辑模式后 在最后一行输入

```shell
export PATH=/root/Swift/swift-5.0.2-RELEASE-ubuntu18.04/usr/bin:"${PATH}"
```

如下图：

![](image_01.png)

圈出来的部分为Swift的bin目录路径，根据自己的路径自行设置

> 保存退出后，更新环境变量

```shell
source /etc/profile
```

## 6.验证成功与否

```shell
swift --version
```

> 看到如下信息表示Swift环境搭建成功

```shell
Swift version 5.0.2 (swift-5.0.2-RELEASE)
Target: x86_64-unknown-linux-gnu
```