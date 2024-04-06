---
title: CSS 干货
pubDatetime: 2023-03-29T03:10:00.000Z
tags:
  - 前端
---

> 文章涉及scss的知识

## 清除浮动

```
@mixin clearfix {
    &:after{
        content: "";
        display: block;
        clear: both;
        visibility: hidden;
        line-height: 0;
        height: 0;
    }
}
```

## 去除数字输入框上下选择按钮

```
input[type="number"] {
    &::-webkit-outer-spin-button, &::-webkit-inner-spin-button {
        -webkit-appearance: none;
    }
    -moz-appearance: textfield;
}
```

## 超出省略

```
@mixin ellipsis($line: 1) {
    overflow: hidden;
    @if $line > 1 {
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: $line;
    } @else {
        text-overflow: ellipsis;
        white-space: nowrap;
    }
}
```

## 解决ios使用overflow: scroll卡顿

```CSS
-webkit-overflow-scrolling: touch;
```

## 去除ios输入框阴影

```
input {
    -webkit-appearance: none;
}
```

## 识别`\n`并成功换行

```
white-space: pre-line;
```

## 浮动排列

```
@mixin sequence($space, $num) {
  $size: percentage(1 / $num);
  width: calc(#{$size} - #{$space} * #{$num - 1} / #{$num});
  float: left;
  margin-top: $space;
  margin-right: $space;
  &:nth-child(-n+#{$num}) {
    margin-top: 0;
  }
  &:nth-child(#{$num}n) {
    margin-right: 0;
  }
}
```

## 底部安全区域

```
@mixin safearea($distance: 0px, $selector: padding-bottom) {
  #{$selector}: $distance;
  #{$selector}: calc(#{$distance} + constant(safe-area-inset-bottom));
  #{$selector}: calc(#{$distance} + env(safe-area-inset-bottom));
}
```
