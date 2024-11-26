---
title: NodeJS 获取拼图验证码滑动距离
pubDatetime: 2024-11-14T10:27:00.000Z
tags:
  - 服务器
---

```ts
import jimp from "jimp";
import axios from "axios";

interface TGetDistanceOptions {
  catpchaUrl: string;
  catpchaWitdh: number;
  catpchaHeight: number;
  slideTop: number;
  slideHeight: number;
}

async function getDistance({
  catpchaUrl,
  catpchaWitdh,
  catpchaHeight,
  slideTop,
  slideHeight,
}: TGetDistanceOptions) {
  const bgImage = await axios
    .get(catpchaUrl, { responseType: "arraybuffer" })
    .then(res => Buffer.from(res.data, "binary"));

  const image = await jimp.read(bgImage);

  image.grayscale(); // 灰度去颜色
  image.contrast(1); // 对比值拉高
  // image.write('./catpcha.jpg') // 生成处理后的图片（查看该图片你就知道原理是啥了）
  image.resize(catpchaWitdh, catpchaHeight);

  const { width, height } = image.bitmap;

  const xList: number[] = [];
  image.scan(0, 0, width, height, (x, y) => {
    if (y >= slideTop && y <= slideTop + slideHeight) {
      const color = image.getPixelColor(x, y);
      if (color === 255) {
        // 黑色
        const _color = image.getPixelColor(x - 2, y);
        if (_color === 4294967295) xList.push(x); // 白色
      }
    }
  });

  return Number(getRepeatMost(xList));
}

function getRepeatMost(arr: number[]) {
  const count: Record<string, number> = {};
  for (let i = 0; i < arr.length; i++) {
    if (count[arr[i]]) {
      count[arr[i]]++;
    } else {
      count[arr[i]] = 1;
    }
  }

  let max = 0;
  let result: string | undefined;
  for (let num in count) {
    if (count[num] > max) {
      max = count[num];
      result = num;
    }
  }

  return result;
}
```

```ts
getDistance({
  catpchaUrl:
    "https://p9-catpcha.byteimg.com/tos-cn-i-188rlo5p4y/e2216ce13cec46fdb4e7ee9dc4d77e73~tplv-188rlo5p4y-2.jpeg",
  catpchaWitdh: 340,
  catpchaHeight: 212,
  slideTop: 82,
  slideHeight: 68,
});
```
