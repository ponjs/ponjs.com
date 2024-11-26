---
title: Typescript 映射类型（Mapped types）
pubDatetime: 2023-04-29T03:20:00.000Z
tags:
  - 前端
---

## Partial

将 T 中的所有属性成为可选

```Typescript
type Partial<T> = {
  [P in keyof T]?: T[P]
}
```

```Typescript
interface T0 {
  x: number
}

type T1 = Partial<T0>
//    ^ = { x?: number }
```

## Required

使 T 中的所有属性成为必选

```Typescript
type Required<T> = {
  [P in keyof T]-?: T[P]
}
```

```Typescript
interface T0 {
  x?: number
}

type T1 = Required<T0>
//    ^ = { x: number }
```

## Readonly

将 T 中的所有属性成为只读

```Typescript
type Readonly<T> = {
  readonly [P in keyof T]: T[P]
}
```

```Typescript
interface T0 {
  x: number
}

type T1 = Readonly<T0>
//    ^ = { readonly x: number }
```

## Pick

从 T 中选择一组键位于联合 K 中的属性

```Typescript
type Pick<T, K extends keyof T> = {
  [P in K]: T[P]
}
```

```Typescript
interface T0 {
  x: number
  y: number
  w: number
  h: number
}

type T1 = Pick<T0, 'x' | 'y'>
//    ^ = { x: number, y: number }
```

## Omit

从 T 中剔除一组键位于联合 K 中的属性

```Typescript
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>
```

```Typescript
interface T0 {
  x: number
  y: number
  w: number
  h: number
}

type T1 = Omit<T0, 'x' | 'y'>
//    ^ = { w: number, h: number }
```

## Record

构造一组属性 K 为 T 类型的类型

```Typescript
type Record<K extends keyof any, T> = {
  [P in K]: T
}
```

```Typescript
type T0 = Record<'x' | 'y', number>
//    ^ = { x: number, y: number }
```

## Exclude

从 T 中剔除可分配给 U 的类型

```Typescript
type Exclude<T, U> = T extends U ? never : T
```

```Typescript
type T0 = 'A' | 'B' | 'C' | 'D'
type T1 = 'A' | 'B'

type T2 = Exclude<T0, T1>
//    ^ = 'C' | 'D'
```

## Extract

从 T 中提取可分配给 U 的类型

```Typescript
type Extract<T, U> = T extends U ? T : never
```

```Typescript
type T0 = 'A' | 'B' | 'C' | 'D'
type T1 = 'A' | 'E'

type T2 = Extract<T0, T1>
//    ^ = 'A'
```

## NonNullable

从 T 中剔除 null 和 undefined

```Typescript
type NonNullable<T> = T extends null | undefined ? never : T
```

```Typescript
type T0 = string | number | undefined | null

type T1 = NonNullable<T0>
//    ^ = string | number
```

## Parameters

获取函数参数类型

```Typescript
type Parameters<T extends (...args: any) => any> = T extends (...args: infer P) => any ? P : never
```

```Typescript
type Func = (a: number, b: number) => number

type FuncPar = Parameters<Func>
//         ^ = [a: number, b: number]
```

## ConstructorParameters

获取构造函数参数类型

```Typescript
type ConstructorParameters<T extends abstract new (...args: any) => any> = T extends abstract new (...args: infer P) => any ? P : never
```

## ReturnType

获取函数类型的返回类型

```Typescript
type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any
```

```Typescript
type Func = (a: number, b: number) => number

type FuncRet = ReturnType<Func>
//         ^ = number
```

## InstanceType

获取构造函数类型的返回类型

```Typescript
type InstanceType<T extends abstract new (...args: any) => any> = T extends abstract new (...args: any) => infer R ? R : any;
```

## ThisParameterType

提取函数类型的 this 参数的类型，如果函数类型没有 this 参数，则为 unknown

```Typescript
type ThisParameterType<T> = T extends (this: infer U, ...args: any[]) => any ? U : unknown
```

## OmitThisParameter

从函数类型中剔除 this 参数

```Typescript
type OmitThisParameter<T> = unknown extends ThisParameterType<T> ? T : T extends (...args: infer A) => infer R ? (...args: A) => R : T
```
