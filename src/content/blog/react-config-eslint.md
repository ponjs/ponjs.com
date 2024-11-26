---
title: react 配置 eslint + prettier
pubDatetime: 2023-06-29T03:16:00.000Z
tags:
  - 前端
---

## 创建 react 项目

```bash
npx create-react-app my-app --template typescript
```

## 配置 eslint

安装依赖

```bash
yarn add eslint -D
```

在项目根目录创建 `.eslintrc.js` 文件

```bash
touch .eslintrc.js
```

将 `package.json` 中的 `eslintConfig` 项删除，迁移到 `.eslintrc.js`

```JavaScript
// .eslintrc.js
/** @type {import('eslint').Linter.Config} */
module.exports = {
  root: true,
  env: {
    node: true,
  },
  extends: [
    'eslint:recommended',
    'react-app',
    'react-app/jest'
  ],
  parserOptions: {
    ecmaVersion: 2020,
    sourceType: 'module',
  },
}
```

注意这里有个坑，创建后的项目默认是有 `react-app` `react-app/jest`，但是如果要支持这两项需要安装[eslint-config-react-app](https://www.npmjs.com/package/eslint-config-react-app)，且不仅安装这一个就行，还要安装其他依赖一起。所以我们这里把这两项删了。但是要支持 `react` 语法，这里我们安装 `eslint-plugin-react` 就行

```bash
yarn add eslint-plugin-react -D
```

```JavaScript
// .eslintrc.js
extends: [
  'eslint:recommended',
  'plugin:react/recommended'
],
settings: {
  react: {
    version: 'detect',
  },
},
```

## 配置 prettier

安装依赖

```bash
yarn add prettier eslint-plugin-prettier eslint-config-prettier -D
```

在项目根目录创建 `.prettierrc.js` 文件

```bash
touch .prettierrc.js
```

下面列出个人的常用配置，更多配置可查看[官方文档](https://prettier.io/docs/en/options.html)

```JSON
// .prettierrc.js
/** @type {import('prettier').Config} */
module.exports = {
  arrowParens: 'avoid',
  endOfLine: 'lf',
  htmlWhitespaceSensitivity: 'ignore',
  printWidth: 100,
  proseWrap: 'never',
  semi: false,
  singleQuote: true,
  tabWidth: 2,
  trailingComma: 'es5',
}
```

配置 `eslint`

```JavaScript
// .eslintrc.js
extends: [
  // ...
  'plugin:prettier/recommended'
],
rules: {
  'prettier/prettier': 'error'
}
```

## 配置 Typescript

安装依赖

```bash
yarn add @typescript-eslint/parser @typescript-eslint/eslint-plugin -D
```

配置 `eslint`

```JavaScript
// .eslintrc.js
extends: [
  // ...
  'plugin:@typescript-eslint/recommended'
]
```

## 配置 scripts

在 `package.json` 文件的 `scripts` 中，加入下面该命令。然后执行 `yarn lint`，就可以格式所有文件

```JSON
{
  "scripts": {
    // ...
    "lint": "eslint --fix ."
  }
}
```

## 汇总

```bash
yarn add eslint eslint-plugin-react prettier eslint-plugin-prettier eslint-config-prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin -D
```

```JavaScript
// .eslintrc.js
/** @type {import('eslint').Linter.Config} */
module.exports = {
  root: true,
  env: {
    node: true,
  },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:prettier/recommended'
  ],
  // parserOptions: {
  //   ecmaVersion: 2020,
  //   sourceType: 'module',
  // },
  rules: {
    'prettier/prettier': 'error',
  },
  settings: {
    react: {
      version: 'detect',
    },
  },
}
```

```JSON
// .prettierrc.js
/** @type {import('prettier').Config} */
module.exports = {
  arrowParens: 'avoid',
  endOfLine: 'lf',
  htmlWhitespaceSensitivity: 'ignore',
  printWidth: 100,
  proseWrap: 'never',
  semi: false,
  singleQuote: true,
  tabWidth: 2,
  trailingComma: 'es5',
}
```
