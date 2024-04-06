---
title: Windows 安装使用 Aria2
pubDatetime: 2023-03-29T02:35:00.000Z
tags:
  - Windows
---

Aria2是一个多平台轻量级，支持多协议、多来源、多线程的命令行下载工具。然而Aria2是一个命令行下载工具，所以使用的时候要敲命令，可是每下载一个文件敲一条命令，太麻烦了。但是Aria2支持远程接口调用，只需要配置一个Web管理面板就可以在浏览器管理。

## 下载相关文件

先去Github下载Aria2最新版，下载地址：[https://github.com/aria2/aria2/releases][1]，根据你电脑系统选择32位还是64位
![][2]

下载完成后解压(平常安装软件的路径)，然后再下载脚本和配置文件：[点击下载][3]，下载完成后解压在`Aria2路径`下
![][4]

```
BaiduExporter    百度云Chrome插件
Download         下载文件夹
aria2.conf       配置文件
aria2.session    下载会话文件
HideRun.vbs      隐藏运行框运行
Start.bat        启动(有运行框)
Status.bat       状态
Stop.bat         停止
```

## 启动

双击`HideRun.vbs`或`Start.bat`即可

## 使用

配合Web面板下载，常用的Aria2Web有[YAAW][5]、[webui-aria2][6]、[AriaNg][7]。你也可以使用我部署的[AriaNg][8]，在Aria2 RPC地址输入`127.0.0.1`或`localhost`保存即可，新建下载输入下载链接(支持磁力链和BT种子)，下载完成存在Aria2路径下的`Download`文件夹
![][9]

## 开机自启

`win+R`打开`运行`对话框，输入`shell:startup`打开`启动文件夹`
右键`HideRun.vbs`创建快捷方式，将该快捷方式移动到`启动文件夹`
![][10]

[1]: https://github.com/aria2/aria2/releases
[2]: @assets/images/windows-using-aria2/1.png
[3]: https://down.ponjs.com/Aria2Win.zip
[4]: @assets/images/windows-using-aria2/2.png
[5]: https://github.com/binux/yaaw
[6]: https://github.com/ziahamza/webui-aria2
[7]: https://github.com/mayswind/AriaNg
[8]: https://aria2.ponjs.com
[9]: @assets/images/windows-using-aria2/3.png
[10]: @assets/images/windows-using-aria2/4.png
