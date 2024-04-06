---

title: MongoDB笔记（二）- 查询文档
pubDatetime: 2023-03-29T03:12:00.000Z
tags:

- 后端
  ---s

```
find(<query>, <projection>)
        |          |
     筛选条件    文档投影
```

读取全部（不筛选不投影）：

```
find()
```

结构化数据展示：

```
find().pretty()
```

匹配查询：

```
{ <field>: <value> }
{ '<object.field>': <value> }
```

## 比较操作符

```
{ <field>: { $<operator>: <value> } }
```

```
$eq     相等
$ne     不等
$gt     大于
$gte    大于或等于
$lt     小于
$lte    小于或等于
$in     包含
        { <field>: { $in: [<value1>, <value2>...] } }
$nin    不包含
        { <field>: { $nin: [<value1>, <value2>...] } }
```

## 逻辑操作符

```
$not    匹配筛选条件不成立的文档
        { <field>: { $not: <operator-expressin> } }
$nor    匹配多个筛选条件全部不成立的文档
        { <field>: { $nor: [<expressin1>, <expressin2>...] } }
$and    匹配多个筛选条件全部成立的文档
        { <field>: { $and: [{ <expressin1> }, { <expressin2> }...] } }
$or     匹配至少一个筛选条件成立的文档
        { <field>: { $or: [{ <expressin1> }, { <expressin2> }...] } }
```

## 字符操作符

```
$exists    匹配包含查询字段的文档
           { <field>: { $exists: <boolean> } }
$type      匹配字段类型符合查询的文档
           { <field>: { $type: <BSON type> } }
           { <field>: { $type: [<BSON type1>, <BSON type2>...] } }
```

## 数组操作符

```
$all          匹配数组字段中包含所有查询值的文档
              { <arryField>: { $all: [<value1>, <value2>...] } }
$elemMatch    匹配数组字段中至少存在一个值满足筛选条件的文档
              { <arryField>: { $elemMatch: { <query1>, <query2>... } } }
```

## 运算操作符

```
$regex:    匹配满足正则表达式的文档
           { <field>: { $regex: /pattern/, $options: '<options>' } }
           { <field>: { $regex: 'pattern', $options: '<options>' } }
           { <field>: { $regex: /pattern/<options> } }
```

注：在和`$in`操作符一起使用时，只能使用`/pattern/<options>`

## 文档游标

```
<cursor>.hasNext()                  判断是否还有更多的文档
         next()                     获取下一条文档
         objsLeftInBatch()          查看当前批次剩余的未被迭代的文档数量
         limit(<number>)            限制结果返回数量
         skip(<offset>)             跳过指定数目的文档
         sort(<document>)           对查询结果进行排序
                                    { <field>: <ordering> }
                                    <ordering>: 1正序 -1倒序
         count(<applySkipLimit>)    获取结果集中总的文档数量
                                    <applySkipLimit>: 默认为false，即不考虑skip和limit的效果（注：在不提供筛选条件时，从集合的元数据Metadata中获取）
```

## 文档投影

```
find(<query>, <projection>)
                   |
                文档投影
```

```
{ <field>: <inclusion> }
                |
            1返回 0不返回
```

在数组上使用

```
$slice             可以返回数组字段中的指定序号元素（可以为负数）
                   { <arryField>: { $slice: <number> } }
                   { <arryField>: { $slice: [<number1>, <number2>...] } }
$elemMatch 和 $    可以返回数组字段中满足筛选条件的第一个元素
                   { <arryField>: { $elemMatch: { <query1>, <query2>... } } }
```

注：`_id`默认总是返回的，若不想返回则`_id: 0`，除`_id: 0`外，其他字段要么统一为`1`要么为`0`，即不可混用
