---
title: vue 配置 eslint + prettier
pubDatetime: 2023-06-29T03:18:00.000Z
tags:
  - 前端
---

vue 项目添加 `eslint` 很简单。你可以在创建项目时可以勾选 `Linter / Formatter`。但如果你是想在原有的项目上添加 `eslint`，只需执行下面命令即可。

## 安装 eslint

```bash
vue add eslint

# ? Pick an ESLint config:
#   Prettier

# ? Pick additional lint features:
#   Lint on save
```

## 配置 prettier

新建 `.prettierrc` 文件，用于配置 `prettier` 格式项。

```bash
touch .prettierrc
```

```JSON
// .prettierrc

{
  "arrowParens": "avoid",
  "endOfLine": "lf",
  "htmlWhitespaceSensitivity": "ignore",
  "printWidth": 100,
  "proseWrap": "never",
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

在 `eslint rules` 里开启 `prettier` 规则。

```JavaScript
// .eslintrc.js

rules: {
  // ...
  'prettier/prettier': 'error'
}
```

## 检查 eslint

将 `eslint` 警告的相关代码调整或添加 `eslint rules`。

```bash
npm run lint
```
