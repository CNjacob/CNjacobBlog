---
title: VPS安装Shadowsocks
date: 2019-07-09 15:33:28
tags: Tool
---

### VPS安装Shadowsocks

下载Shadowsocks
```shell
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
```

添加可执行权限
```shell
chmod +x shadowsocks-all.sh
```

配置
```shell
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

<!--more-->

选择脚本（Python、R、Go、libev）,任选一个:
```shell
Which Shadowsocks server you'd select:
1) Shadowsocks-Python
2) ShadowsocksR
3) Shadowsocks-Go
4) Shadowsocks-libev
Please enter a number (Default Shadowsocks-Python):3

You choose = Shadowsocks-Go
```
我这里选择的的Shadowsocks-Go

设置密码:
```shell
Please enter password for Shadowsocks-Go
(Default password: teddysun.com):
```

设置端口号:
```shell
Please enter a port for Shadowsocks-Go [1-65535]
(Default port: 13412):
```

选择加密方式:
```shell
Please select stream cipher for Shadowsocks-Go:
1) aes-256-cfb
2) aes-192-cfb
3) aes-128-cfb
4) aes-256-ctr
5) aes-192-ctr
6) aes-128-ctr
7) chacha20-ietf
8) chacha20
9) salsa20
10) rc4-md5
Which cipher you'd select(Default: aes-256-cfb):1

cipher = aes-256-cfb


Press any key to start...or Press Ctrl+C to cancel
```

看到以下信息表示安装完成。 * 部分是自己的服务器IP 端口号 密码
```shell
Congratulations, Shadowsocks-Go server install completed!
Your Server IP        :  * 
Your Server Port      :  * 
Your Password         :  * 
Your Encryption Method:  aes-256-cfb 

Your QR Code: (For Shadowsocks Windows, OSX, Android and iOS clients)
 ss://YWVzLTI1Ni1jZmI6SmFjb2JAMTEyMUAyMDcuMjQ2Ljk4LjE3NDo0NDM= 
Your QR Code has been saved as a PNG file path:
 /root/software/Shadowsocks/shadowsocks_go_qr.png 

Welcome to visit: https://teddysun.com/486.html
Enjoy it!
```