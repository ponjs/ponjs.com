---
title: ShadowsocksR 一键安装脚本
pubDatetime: 2023-03-29T03:00:00.000Z
tags:
  - 服务器
---

## 脚本说明

系统支持：CentOS，Debian，Ubuntu
内存要求：≥128M
作者：[teddysun][1]

## 配置说明

服务器端口：自己设定（如不设定，默认为随机）
密码：自己设定（如不设定，默认为 teddysun.com）
加密方式：自己设定（如不设定，默认为 aes-256-cfb）
协议（Protocol）：自己设定（如不设定，默认为 origin）
混淆（obfs）：自己设定（如不设定，默认为 plain）

## 配置方法

使用`root`用户登录，执行以下命令：

```
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
chmod +x shadowsocksR.sh
./shadowsocksR.sh 2>&1 | tee shadowsocksR.log
```

CentOS 7系统如出现`-bash: wget: command not found`错误请先执行以下命令安装`wget`

```
yum -y install wget
```

安装完成后，脚本提示如下：

```
Congratulations, ShadowsocksR server install completed!
Your Server IP        :your_server_ip
Your Server Port      :your_server_port
Your Password         :your_password
Your Protocol         :your_protocol
Your obfs             :your_obfs
Your Encryption Method:your_encryption_method
Welcome to visit:https://shadowsocks.be/9.html
Enjoy it!
```

本脚本安装完成后，已将`ShadowsocksR`启动并自动加入开机自启动

## 卸载方法

使用`root`用户登录，运行以下命令：

```
./shadowsocksR.sh uninstall
```

## 使用命令

```
启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
状态：/etc/init.d/shadowsocks status
配置文件路径：/etc/shadowsocks.json
日志文件路径：/var/log/shadowsocks.log
代码安装目录：/usr/local/shadowsocks
```

## 多用户配置示例

```
{
    "server": "0.0.0.0",
    "server_ipv6": "[::]",
    "local_address": "127.0.0.1",
    "local_port": 1080,
    "port_password": {
        "8989": "password1",
        "8990": "password2",
        "8991": "password3"
    },
    "timeout": 300,
    "method": "aes-256-cfb",
    "protocol": "origin",
    "protocol_param": "",
    "obfs": "plain",
    "obfs_param": "",
    "redirect": "",
    "dns_ipv6": false,
    "fast_open": false,
    "workers": 1
}
```

## 客户端下载

[Windows][2] [Android][3]

[1]: https://github.com/teddysun/shadowsocks_install/tree/master
[2]: https://github.com/shadowsocksrr/shadowsocksr-csharp/releases
[3]: https://github.com/shadowsocksrr/shadowsocksr-android/releases
