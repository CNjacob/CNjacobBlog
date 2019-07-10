---
title: CentOS安装Tomcat
date: 2019-07-10 11:46:51
tags: Notes
---

## 1.安装tomcat
安装tomcat之前，需要先安装JDK，[安装JDK][1]参考：

官网下载[tomcat][2]


[1]: https://cnjacob.com/2019/03/11/2019-07-10-Notes-CentOS安装JDK
[2]: https://tomcat.apache.org/download-90.cgi

<!--more-->

创建一个文件夹用于存放tomcat安装包

```shel
cd root/
mkdir software
cd software/
mkdir tomcat
cd tomcat
```

将下载的tomcat安装包放置到 `/root/software/tomcat` 下

解压安装包，解压完成后再删除安装包

```shell
tar -zxvf apache-tomcat-9.0.21.tar.gz
rm apache-tomcat-9.0.21.tar.gz
```
将解压后的文件夹重命名为 `tomcat9`

```shell
mv /root/software/tomcat/apache-tomcat-9.0.12 /root/software/tomcat/tomcat9
```

## 2.配置自启动
切换至Tomcat的bin目录执行vi setenv.sh

```shell
cd tomcat9/bin
vi setenv.sh
```

按i进入编辑模式，拷贝以下代码粘贴，然后保存退出

```shell
#add tomcat pid
CATALINA_PID="$CATALINA_BASE/tomcat.pid"
#add java opts
JAVA_OPTS="-server -XX:PermSize=256M -XX:MaxPermSize=1024m -Xms512M -Xmx1024M -XX:MaxNewSize=256m"
```

确保文件setenv.sh可执行

```shell
chmod +x setenv.sh
```

## 3.配置service，开机启动

```shell
cd /usr/lib/systemd/system
vi tomcat.service
```
也可以直接
```shell
vi /usr/lib/systemd/system/tomcat.service
```

按i进入编辑模式，拷贝以下代码粘贴，然后保存退出
> 注意将第6和7行的tomcat路径 `/root/software/tomcat/tomcat9` 换成你自己的tomcat的绝对路径
```shell
[Unit]
Description=Tomcat
After=syslog.target network.target remote-fs.target nss-lookup.target
[Service]
Type=forking
PIDFile=/root/software/tomcat/tomcat9/tomcat.pid
ExecStart=/root/software/tomcat/tomcat9/bin/startup.sh
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true
[Install]
WantedBy=multi-user.target
```

执行以下指令将tomcat.service添加开机至开机启动

配置开机启动

```shell
systemctl enable tomcat
```
启动tomcat

```shell
systemctl start tomcat
```
停止tomcat

```shell
systemctl stop tomcat
```

重启tomcat

```shell
systemctl restart tomcat
```
当然启动和结束tomcat也可以在tomcat的安装目录的bin目录下执行 `./shutdown.sh` 和 `./startup.sh` 来完成。

配置完成，建议重启服务器，即输入命令 `reboot` 或者 `sudo reboot`

## 4.配置tomcat被外部访问
> 在linux上开启的tomcat使用浏览器访问不了。主要原因在于防火墙的存在，导致的端口无法访问。CentOS7使用firewall而不是iptables。所以解决这类问题可以通过添加firewall的端口，使其对我们需要用的端口开放。

查看防火墙状态，得到结果是running或者not running

```shell
firewall-cmd --state
```

在running 状态下，向firewall 添加需要开放的端口
永久的添加8080端口,去掉 `--permanent` 则表示临时

```shell
firewall-cmd --permanent --zone=public --add-port=8080/tcp
```

加载配置，使得修改有效

```shell
firewall-cmd --reload
```

查看开启的端口

```shell
firewall-cmd --permanent --zone=public --list-ports
```

### 5.补充

> CentOS7以下有专门的防火墙操作命令
开启防火墙

```shell
systemctl start firewalld.service
```

关闭防火墙

```shell
systemctl stop firewalld.service
```

开机自动启动

```shell
systemctl enable firewalld.service
```

关闭开机启动

```shell
systemctl disable firewalld.service
```

查看防火墙状态

```shell
systemctl status firewalld
```
