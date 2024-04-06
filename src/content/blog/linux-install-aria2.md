---
title: Linux 安装 Aria2
pubDatetime: 2023-03-29T01:35:00.000Z
tags:
  - 服务器
---

## 说明

Aria2 是一款使用 C++ 编写的轻量级跨平台命令行下载工具，支持 HTTP/HTTPS, FTP, SFTP, BitTorrent 和 Metalink 等多种协议。该脚本只是安装Aria2服务端，安装后默认会启动，但是还需要前端面板配合使用，如 Aria2 Web UI 或 AriaNG 等等。

## 一键脚本安装

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/aria2.sh && chmod +x aria2.sh && bash aria2.sh
```

运行脚本后会出现脚本操作菜单，选择并输入`1`就会开始安装

## 使用说明

运行脚本

```bash
./aria2.sh 或 bash aria2.sh
```

然后选择你要执行的选项即可

```
Aria2 一键安装管理脚本 [vx.x.x]
-- Toyo | doub.io/shell-jc4 --

 0. 升级脚本
————————————
 1. 安装 Aria2
 2. 更新 Aria2
 3. 卸载 Aria2
————————————
 4. 启动 Aria2
 5. 停止 Aria2
 6. 重启 Aria2
————————————
 7. 修改 配置文件
 8. 查看 配置信息
 9. 查看 日志信息
10. 配置 自动更新 BT-Tracker服务器
————————————

当前状态: 已安装 并 已启动

请输入数字 [0-10]:
```

## 其他操作

```
启动：/etc/init.d/aria2 start
停止：/etc/init.d/aria2 stop
重启：/etc/init.d/aria2 restart
查看状态：/etc/init.d/aria2 status
配置文件：/root/.aria2/aria2.conf （配置文件包含中文注释，但是一些系统可能不支持显示中文）
令牌密匙：随机生成（可以自己修改 7. 修改 配置文件）
下载目录：/usr/local/caddy/www/aria2/Download（默认路径，可修改）
```
