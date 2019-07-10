---
title: CentOS安装JDK
date: 2019-07-10 11:46:36
tags: Notes
---

查看yum库中的Java安装包：
```shell
yum -y list java*
```

安装需要的jdk版本的所有Java程序：
```shell
yum -y install java-1.8.0-openjdk*
```

<!--more-->

安装完成后查看Java版本：
```shell
java -version
```

卸载对应jdk版本的所有Java程序：
```shell
yum -y remove java-1.8.0-openjdk*
```