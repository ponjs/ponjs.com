---
title: Linux 开启 bbr 加速
pubDatetime: 2023-03-29T05:54:00.000Z
tags:
  - 服务器
---

一键安装脚本

```bash
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```

如果是低版本的 centos 可能需要清除缓存（一般不用）

```
rm -rf /var/lib/yum/history/*.sqlite
```

安装完成后重启并验证

```
sudo reboot
sysctl net.ipv4.tcp_available_congestion_control
sysctl net.ipv4.tcp_congestion_control
sysctl net.core.default_qdisc
lsmod | grep bbr
```
