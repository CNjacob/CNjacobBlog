---
title: Hexo简单使用
date: 2019-03-11 10:43:38
tags: Notes
author: "Jacob"
---

## 新建文章
```shell
# 新建一篇文章 post类型 年-月-日-标签类型-标题
hexo new post 2019-03-11-Tool-Hexo
```

<!--more-->

## 预览
```shell
hexo s
# 预览DEBUG模式
hexo s -debug
```

## 生成静态网页文件
```shell
# 会在根目录下生成一个 public 文件夹
hexo g
```

## 清理
```shell
# 会删除根目录下的 public 文件夹
hexo clean
```

## 部署
部署之前不想覆盖 README.md 文件，在生成静态网页文件后，将根目录下的 README.md 文件拷贝到 public 文件夹，并删除 README.html 文件
```shell
hexo d
```
