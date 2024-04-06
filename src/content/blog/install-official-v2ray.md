---
title: 安装官方 V2Ray
pubDatetime: 2023-03-29T02:52:00.000Z
tags:
  - 服务器
---

## 说明

V2Ray 提供了一个在 Linux 中的自动化安装脚本。这个脚本会自动检测有没有安装过 V2Ray，如果没有，则进行完整的安装和配置；如果之前安装过 V2Ray，则只更新 V2Ray 二进制程序而不更新配置。[官网][1]提供了详细的文档参考，这里就以最简单的方式安装。

## 安装

运行下面的指令下载并安装 V2Ray

```
bash <(curl -L -s https://install.direct/go.sh)
```

此脚本会自动安装以下文件：

```
/usr/bin/v2ray/v2ray      ：V2Ray 程序；
/usr/bin/v2ray/v2ctl      ：V2Ray 工具；
/etc/v2ray/config.json    ：配置文件；
/usr/bin/v2ray/geoip.dat  ：IP 数据文件
/usr/bin/v2ray/geosite.dat：域名数据文件
```

你可以选择性编辑`/etc/v2ray/config.json`文件来配置你需要的代理方式
然后运行下面指令启动 V2Ray 进程

```
service v2ray start
```

## 使用命令

之后可以使用下面指令控制 V2Ray 的运行。

```
service v2ray start|stop|status|reload|restart|force-reload
```

## go.sh 参数

go.sh 支持如下参数，可在手动安装时根据实际情况调整：

```
-p 或 --proxy: 使用代理服务器来下载 V2Ray 的文件，格式与 curl 接受的参数一致，比如 "socks5://127.0.0.1:1080" 或 "http://127.0.0.1:3128"。
-f 或 --force: 强制安装。在默认情况下，如果当前系统中已有最新版本的 V2Ray，go.sh 会在检测之后就退出。如果需要强制重装一遍，则需要指定该参数。
--version    : 指定需要安装的版本，比如 "v1.13"。默认值为最新版本。
--local      : 使用一个本地文件进行安装。如果你已经下载了某个版本的 V2Ray，则可通过这个参数指定一个文件路径来进行安装。
```

## 客户端

[v2rayN （Windows）][2]
[v2rayX （Mac）][3]
[v2rayNG（Android）][4]

[1]: https://www.v2ray.com/
[2]: https://github.com/2dust/v2rayN/releases
[3]: https://github.com/Cenmrev/V2RayX/releases
[4]: https://github.com/2dust/v2rayNG/releases
