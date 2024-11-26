---
title: 在 Linux 运行 puppeteer 避坑指南
pubDatetime: 2024-09-29T03:21:10.000Z
tags:
  - 服务器
---

**error while loading shared libraries: libatk-1.0.so.0: cannot open shared object file: No such file or directory**

> 加载共享库时出错：libatk-1.0.so.0：无法打开共享对象文件：没有这样的文件或目录

意思就是打开不了 `chrome` 或 `chromium`，所以这里我安装一下 `google-chrome`：

```bash
# centos
wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
sudo yum localinstall google-chrome-stable_current_x86_64.rpm

# ubuntu
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
# sudo sh -c 'echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update
sudo apt-get install google-chrome-stable
```

**Running as root without --no-sandbox is not supported. See https://crbug.com/638180.**

> 不支持以 root 身份运行而不使用 --no-sandbox。见 https://crbug.com/638180。

在 `puppeteer.launch` 补充参数：

```js
const browser = await puppeteer.launch({
  args: ["--no-sandbox", "--disable-setuid-sandbox"],
});
```

**Missing X server or $DISPLAY**

> 缺少 X server 或 $DISPLAY

是因为我这里启动配置中 `headless: false` 所以提示缺少图形界面，解决方法可以开启无头或加个显示服务器。

```bash
yum install Xvfb

# 这里的 node index.js 为执行文件命令
xvfb-run --auto-servernum node index.js
```
