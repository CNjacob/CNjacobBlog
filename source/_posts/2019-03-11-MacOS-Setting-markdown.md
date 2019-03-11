---
title: Mac OS X 设置所有来源
date: 2019-03-11 10:25:41
tags: Mac OS
---

设置Mac OS允许所有来源

```shell
# 开启允许所有来源
sudo spctl --master-disable
# 关闭允许所有来源
sudo spctl --master-enable
```