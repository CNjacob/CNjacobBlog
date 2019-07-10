---
title: Hexo图片显示
date: 2019-03-27 16:56:58
tags: Notes
author: "CNjacob"
---

![](example.jpg)

<!--more-->

## 1.设置站点配置_config.yml
```
post_asset_folder: true
```

此时运行hexo new post "xxxx"来生成md博文时，/source/_posts文件夹内除了xxxx.md文件还有一个同名的文件夹

## 2.安装插件
```shell
npm install hexo-asset-image-fixed --save
```

## 3.引用图片
在xxxx.md中想引入图片时，先把图片复制到xxxx这个文件夹中，然后只需要在xxxx.md中按照markdown的格式引入图片

```
![](图片名.jpg)
```

