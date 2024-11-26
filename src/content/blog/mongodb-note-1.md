---
title: MongoDB笔记（一）- 创建文档
pubDatetime: 2024-05-29T03:11:00.000Z
tags:
  - 后端
---

## insertOne 创建单个文档

```
insertOne(<document>, { writeConcern: <document> })
              |              |
          要创建的文档    创建文档操作的安全些级别（一般默认）
```

## insertMany 创建多个文档

```
insertMany([<document1>, <document2>...], { writeConcern: <document>, ordered: <boolean> })
                                                                         |
                                                                      是否按写顺序写入（默认true）
```

注：遇到创建错误时，后面的插入会被中断

## insert 创建单个或多个文档

```
insert(<document or array of documents>, { writeConcern: <document>, ordered: <boolean> })
```

注：`insertOne` `insertMany`不支持`explain()`，但`insert`支持

## save 创建单个文档

```
save(<document>, { writeConcern: <document> })
```
