---
title: Axios 使用
pubDatetime: 2023-03-29T01:34:00.000Z
tags:
  - 前端
---

## 处理图片文件流

```js
axios
  .get(url, {
    responseType: "arraybuffer",
  })
  .then(res => {
    let base64 = btoa(
      new Uint8Array(res.data).reduce(
        (data, byte) => data + String.fromCharCode(byte),
        ""
      )
    );
    return "data:image/png;base64," + base64;
  });
```

然后将返回的字符串赋值到 `img` 标签的 `src` 属性中即可

## 使用qs序列化请求参数

首先安装qs

```bash
npm install qs
```

然后在`axios.js`中引入`qs`

```js
import qs from "qs";
```

配置 axio s的请求拦截器 `interceptors.request`

```js
_axios.interceptors.request.use(config => {
  config.transformRequest = [(data, headers) => qs.stringify(data)];
  return config;
});
```
