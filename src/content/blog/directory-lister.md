---
title: 分享一个 Directory Lister 修改版
pubDatetime: 2024-03-29T02:50:00.000Z
tags:
  - 服务器
---

## 说明

[官方版本][1]由于用了谷歌字体、js等之类的，导致打开特别慢，而且对中文的支持不是很好。这里分享优化的2.6.1版本

## 修改

整理所有的css/js文件到本地，去掉google字体
添加了flat-ui效果
目录伪静态，原：/?dir=path改后：/path/
添加nginx.conf伪静态
修复中文乱码问题

## 使用

Nginx伪静态规则

```
location / {
  rewrite /(.*)/$ /index.php?dir=$1 last;
}
```

修改页头`/resources/themes/bootstrap/default_header.php`
修改页尾`/resources/themes/bootstrap/default_footer.php`

## 演示

[https://down.ponjs.com][2]

## 下载

[Directory Lister.zip][3]

[1]: https://www.directorylister.com
[2]: https://down.ponjs.com
[3]: https://down.ponjs.com/DirectoryLister.zip
