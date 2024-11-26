---
title: AriaNg 使用 Https 或 WebSocket 安全协议连接 Aria2
pubDatetime: 2024-03-29T02:31:00.000Z
tags:
  - 服务器
---

AriaNg算是Aira2中博主认为最好用的一个Web前端面板，连接支持Http(s)或Websocket(Security)协议，如果我们使用https域名访问AriaNg面板，那会强制你使用Https和Websocket(安全)协议，最早期的面板是不会强制的，不过用的话，肯定是用最新版的，这时候就需要对Aria2简单的配下证书了，然后才能使用Https、Websocket(安全)协议进行连接。

## 申请SSL证书

> 提示：如果安装Aria2的服务器有现成的HTTPS站点，可以跳过该步骤，直接使用该站点域名。

这里以宝塔为例：`站点设置 => SSL => 申请Let's Encrypt`

crt证书文件路径（站点配置文件的`ssl_certificate`）：

```
/www/server/panel/vhost/cert/example.com/fullchain.pem
```

key证书文件路径（站点配置文件的`ssl_certificate_key`）：

```
/www/server/panel/vhost/cert/example.com/privkey.pem
```

## 修改配置文件

打开Aria2的配置文件，如果你是根据 [Linux安装Aria2][1] 安装的Aria2，则配置文件在`/root/.aria2/aria2.conf`
修改如下：

```
# 是否启用 RPC 服务的 SSL/TLS 加密,
# 启用加密后 RPC 服务需要使用 https 或者 wss 协议连接
rpc-secure=true
# 在 RPC 服务中启用 SSL/TLS 加密时的证书文件(.pem/.crt)
rpc-certificate=/www/server/panel/vhost/cert/example.com/fullchain.pem
# 在 RPC 服务中启用 SSL/TLS 加密时的私钥文件(.key)
rpc-private-key=/www/server/panel/vhost/cert/example.com/privkey.pem
```

如果配置文件没有以上参数的，可以手动添加，修改完成后，重启Aria2生效即可，此时Https和Websocket(安全)协议就都可以用了，然后AriaNg配置RPC信息的时候，直接填写域名、密匙即可。

[1]: https://ponjs.com/archives/11.html
