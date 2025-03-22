---
title: 使用 WARP 解锁 ChatGPT 访问
pubDatetime: 2025-03-22T10:33:54.794Z
tags:
  - 服务器
---

## 安装 WARP

[官方安装使用教程](https://developers.cloudflare.com/warp-client/get-started/linux/)

## 配置 WARP

```bash
# 注册客户端
warp-cli registration new

# 设置为代理模式
warp-cli set-mode proxy

# 连接 默认为 40000 端口
warp-cli connect
```

## 配置 xray

添加下面配置

```jsonc
{
  "outbounds": {
    {
      "protocol": "socks",
      "tag": "WARP", // 标签名可自定义
      "settings": {
        "servers": [
          {
            "address": "127.0.0.1",
            "port": 40000
          }
        ]
      }
    }
  },
  "routing": {
    "rules": [
      {
        "domain": [
          "geosite:openai"
        ],
        "outboundTag": "WARP", // 这里对应上面 outbounds 里的 tag
        "inboundTag": [
          "xxx" // 这里 xxx 对应 inbounds 里的 tag
        ],
        "type": "field"
      }
    ]
  }
}
```
