---
title: 解决 Windows 下执行命令无法识别错误
pubDatetime: 2023-03-29T03:20:10.000Z
tags:
  - Windows
---

对于 `npm` 安装了全局的 `yarn`，可能出现下面错误：

```bash
yarn : 无法将“yarn”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径正确，然后再试一次。
```

解决方法：
打开 `Windows PowerShell (管理员)` 输入：

```bash
set-ExecutionPolicy RemoteSigned
```

然后输入 `Y` 或 `A` 即可。
