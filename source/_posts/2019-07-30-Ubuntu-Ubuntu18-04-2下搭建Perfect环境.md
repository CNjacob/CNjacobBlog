---
title: Ubuntu18.04.2下搭建Perfect环境
date: 2019-07-30 15:30:15
tags: Ubuntu
---

> 搭建环境 Ubuntu18.04.2 + swift5.0.2 + Mysql5.7

<!--more-->

## 1.前置条件

> Swift环境搭建，参照前面的文章[Ubuntu18.04.2下的Swift环境搭建][1]

> 若需要使用Mysql，可参照前面的文章[Ubuntu18.04.2下安装Mysql5.7][2]，注意⚠️目前Perfect必须Mysql5.7

[1]: https://cnjacob.com/2019/07/30/2019-07-30-Ubuntu-Ubuntu18-04-2下的Swift环境搭建
[2]: https://cnjacob.com/2019/07/30/2019-07-30-Ubuntu-Ubuntu18-04-2下安装Mysql5-7

## 2.安装依赖库

```shell
apt-get install openssl libssl-dev uuid-dev
```

## 3.测试一下

> 创建Perfect目录

```shell
mkdir Perfect
cd Perfect/
```

> 下载Perfect提供的测试Demo

```shell
git clone https://github.com/PerfectlySoft/PerfectTemplate.git
```

```shell
swift build
```

> 编译过程可看到如下信息

```shell
Fetching https://github.com/PerfectlySoft/Perfect-HTTPServer.git
Fetching https://github.com/PerfectlySoft/Perfect-Net.git
Fetching https://github.com/PerfectlySoft/Perfect-HTTP.git
Fetching https://github.com/PerfectlySoft/Perfect-CZlib-src.git
Fetching https://github.com/PerfectlySoft/Perfect-Crypto.git
Fetching https://github.com/PerfectlySoft/Perfect-LinuxBridge.git
Fetching https://github.com/PerfectlySoft/Perfect-Thread.git
Fetching https://github.com/PerfectlySoft/PerfectLib.git
Fetching https://github.com/PerfectlySoft/Perfect-COpenSSL-Linux.git
Completed resolution in 5.97s
Cloning https://github.com/PerfectlySoft/Perfect-HTTP.git
Resolving https://github.com/PerfectlySoft/Perfect-HTTP.git at 3.2.6
Cloning https://github.com/PerfectlySoft/Perfect-CZlib-src.git
Resolving https://github.com/PerfectlySoft/Perfect-CZlib-src.git at 0.0.4
Cloning https://github.com/PerfectlySoft/Perfect-COpenSSL-Linux.git
Resolving https://github.com/PerfectlySoft/Perfect-COpenSSL-Linux.git at 4.0.1
Cloning https://github.com/PerfectlySoft/Perfect-Thread.git
Resolving https://github.com/PerfectlySoft/Perfect-Thread.git at 3.0.7
Cloning https://github.com/PerfectlySoft/Perfect-LinuxBridge.git
Resolving https://github.com/PerfectlySoft/Perfect-LinuxBridge.git at 3.1.0
Cloning https://github.com/PerfectlySoft/Perfect-HTTPServer.git
Resolving https://github.com/PerfectlySoft/Perfect-HTTPServer.git at 3.0.23
Cloning https://github.com/PerfectlySoft/Perfect-Net.git
Resolving https://github.com/PerfectlySoft/Perfect-Net.git at 3.3.0
Cloning https://github.com/PerfectlySoft/PerfectLib.git
Resolving https://github.com/PerfectlySoft/PerfectLib.git at 3.1.4
Cloning https://github.com/PerfectlySoft/Perfect-Crypto.git
Resolving https://github.com/PerfectlySoft/Perfect-Crypto.git at 3.2.0
/root/Perfect/PerfectTemplate/.build/checkouts/PerfectLib/Sources/PerfectLib/Dir.swift:129:16: warning: 'readdir_r' is deprecated
        return readdir_r(d, &dirEnt, endPtr)
               ^
/root/Perfect/PerfectTemplate/.build/checkouts/Perfect-Net/Sources/PerfectNet/NetTCPSSL.swift:219:42: warning: 'TLSv1_2_method()' is deprecated
                case .tlsV1_2: newSslCtx = SSL_CTX_new(TLSv1_2_method())
                                                       ^
/root/Perfect/PerfectTemplate/.build/checkouts/Perfect-Net/Sources/PerfectNet/NetTCPSSL.swift:220:42: warning: 'TLSv1_1_method()' is deprecated
                case .tlsV1_1: newSslCtx = SSL_CTX_new(TLSv1_1_method())
                                                       ^
/root/Perfect/PerfectTemplate/.build/checkouts/Perfect-Net/Sources/PerfectNet/NetTCPSSL.swift:221:40: warning: 'TLSv1_method()' is deprecated
                case .tlsV1: newSslCtx = SSL_CTX_new(TLSv1_method())
                                                     ^
/root/Perfect/PerfectTemplate/.build/checkouts/Perfect-HTTP/Sources/PerfectHTTP/HTTPHeaders.swift:41:15: warning: 'Hashable.hashValue' is deprecated as a protocol requirement; conform type 'HTTPRequestHeader.Name' to 'Hashable' by implementing 'hash(into:)' instead
                        public var hashValue: Int {
                                   ^
/root/Perfect/PerfectTemplate/.build/checkouts/Perfect-HTTP/Sources/PerfectHTTP/HTTPHeaders.swift:242:15: warning: 'Hashable.hashValue' is deprecated as a protocol requirement; conform type 'HTTPResponseHeader.Name' to 'Hashable' by implementing 'hash(into:)' instead
                        public var hashValue: Int {
                                   ^
/root/Perfect/PerfectTemplate/.build/checkouts/Perfect-HTTP/Sources/PerfectHTTP/HTTPMethod.swift:67:14: warning: 'Hashable.hashValue' is deprecated as a protocol requirement; conform type 'HTTPMethod' to 'Hashable' by implementing 'hash(into:)' instead
                public var hashValue: Int {
                           ^
/root/Perfect/PerfectTemplate/.build/checkouts/Perfect-HTTPServer/Sources/PerfectHTTPServer/HTTP2/HTTP2Session.swift:73:7: warning: 'Hashable.hashValue' is deprecated as a protocol requirement; conform type 'HTTP2Session' to 'Hashable' by implementing 'hash(into:)' instead
                var hashValue: Int { return Int(net.fd.fd) }
                    ^
[25/25] Linking ./.build/x86_64-unknown-linux/debug/PerfectTemplate
```

> 没有发现error信息，warning先忽略

> 运行测试Demo

```shell
.build/debug/PerfectTemplate
```

> 看到如下信息，运行成功

```shell
[INFO] Starting HTTP server localhost on :::8181
```

打开浏览器输入服务器ip+端口号查看，如下图所示：

![](image_01.png)
