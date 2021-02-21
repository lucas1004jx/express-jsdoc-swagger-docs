![npm](https://img.shields.io/npm/v/express-jsdoc-swagger)
![Node.js包](https://github.com/BRIKEV/express-jsdoc-swagger/workflows/Build/badge.svg)
[![已知漏洞](https://snyk.io/test/github/BRIKEV/express-jsdoc-swagger/badge.svg)](https://snyk.io/test/github/BRIKEV/express-jsdoc-swagger)
[![维护](https://api.codeclimate.com/v1/badges/6d5565df0c9c10e75b59/maintainability)](https://codeclimate.com/github/BRIKEV/express-jsdoc-swagger/maintainability)
[![测试覆盖](https://api.codeclimate.com/v1/badges/6d5565df0c9c10e75b59/test_coverage)](https://codeclimate.com/github/BRIKEV/express-jsdoc-swagger/test_coverage)
![许可: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![npm](https://img.shields.io/npm/dm/express-jsdoc-swagger)

# express-jsdoc-swagger

使用该库，你可以直接使用 swagger [OpenAPI 3 Specification](https://swagger.io/specification/)来记录你的服务端接口， 而不必使用 YAML 或者 JSON。你可以为每个接口添加 jsdoc 注释， swagger UI 界面将会自动生成。

## 使用条件

使用条件:

1. [NodeJS](https://nodejs.org)
2. [Express.js](http://www.expressjs.com)

## 如何安装

```
npm i express-jsdoc-swagger
```

## 使用方法

```javascript
const express = require("express");
const expressJSDocSwagger = require("express-jsdoc-swagger");

const options = {
  info: {
    version: "1.0.0",
    title: "Albums store",
    license: {
      name: "MIT",
    },
  },
  security: {
    BasicAuth: {
      type: "http",
      scheme: "basic",
    },
  },
  filesPattern: "./**/*.js", // 找到所有jsdoc文件
  swaggerUIPath: "/your-url", // 定义SwaggerUI界面所在的URL。默认为: '/api-docs'
  baseDir: __dirname,
};

const app = express();
const PORT = 3000;

expressJSDocSwagger(app)(options);

/**
 * GET /api/v1
 * @summary 端点的概述
 * @return {object} 200 - 成功回复
 */
app.get("/api/v1", (req, res) =>
  res.json({
    success: true,
  })
);

app.listen(PORT, () =>
  console.log(`Example app listening at http://localhost:${PORT}`)
);
```

## 实例

1. 基础设置

```javascript
const options = {
  info: {
    version: "1.0.0",
    title: "Albums store",
    license: {
      name: "MIT",
    },
  },
  security: {
    BasicAuth: {
      type: "http",
      scheme: "basic",
    },
  },
  filesPattern: "./**/*.js", // 找到所有的jsdoc文件
  baseDir: __dirname,
};
```

2. 定义组件

```javascript
/**
 * 歌曲类型
 * @typedef {object} Song
 * @property {string} title.required - 标题
 * @property {string} artist - 艺术家
 * @property {number} year - 年份 - double
 */
```

3. 一个返回`歌曲类型`的数组的端点

```javascript
/**
 * GET /api/v1/albums
 * @summary 端点的概述
 * @tags 专辑
 * @return {array<Song>} 200 - 回复成功 - application/json
 */
app.get("/api/v1/albums", (req, res) =>
  res.json([
    {
      title: "abum 1",
    },
  ])
);
```

4. 端点的标签，参数和认证的基本定义方法

```javascript
/**
 * GET /api/v1/album
 * @summary 端点的概述
 * @security BasicAuth
 * @tags 专辑
 * @param {string} name.query.required - 名字参数描述
 * @return {object} 200 - 回复成功 - application/json
 * @return {object} 400 - 回复不成功
 */
app.get("/api/v1/album", (req, res) =>
  res.json({
    title: "abum 1",
  })
);
```

5. 端点中网络回复主体实例的基本定义方法

```javascript
/**
 * GET /api/v1/albums
 * @summary 端点的概述
 * @tags 专辑
 * @return {array<Song>} 200 - 回复成功 - application/json
 * @example response - 200 - 回复成功实例
 * [
 *   {
 *     "title": "Bury the light",
 *     "artist": "Casey Edwards ft. Victor Borba",
 *     "year": 2020
 *   }
 * ]
 */
app.get("/api/v1/albums", (req, res) =>
  res.json([
    {
      title: "track 1",
    },
  ])
);
```

在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/tree/master/examples)你可以参考更多的例子。

## 贡献者 ✨

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/bri06"><img src="https://avatars0.githubusercontent.com/u/24435223?v=4" width="100px;" alt=""/><br /><sub><b>Briam Martinez Escobar</b></sub></a><br /><a href="https://github.com/BRIKEV/express-jsdoc-swagger/commits?author=bri06" title="Code">💻</a></td>
    <td align="center"><a href="https://twitter.com/kjmesc"><img src="https://avatars2.githubusercontent.com/u/12685053?v=4" width="100px;" alt=""/><br /><sub><b>Kevin Julián Martínez Escobar</b></sub></a><br /><a href="https://github.com/BRIKEV/express-jsdoc-swagger/commits?author=kevinccbsg" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/hoonga"><img src="https://avatars3.githubusercontent.com/u/10708927?v=4" width="100px;" alt=""/><br /><sub><b>Heung-yeon Oh</b></sub></a><br /><a href="https://github.com/BRIKEV/express-jsdoc-swagger/commits?author=hoonga" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/LonelyPrincess"><img src="https://avatars1.githubusercontent.com/u/17673317?v=4" width="100px;" alt=""/><br /><sub><b>Sara Hernández</b></sub></a><br /><a href="https://github.com/BRIKEV/express-jsdoc-swagger/commits?author=LonelyPrincess" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

该项目依据 [所有贡献着](https://github.com/all-contributors/all-contributors)的规定. 欢迎参与我们的项目！
