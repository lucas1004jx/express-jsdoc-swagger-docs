# 安全

为了通过 express-jsdoc-swagger，为你的网络端点添加 [验证](https://swagger.io/docs/specification/authentication/), 你必须在创建实例的时候，在配置文件里定义安全模式:

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
  filesPattern: "./basic-auth.js",
  baseDir: __dirname,
};

const app = express();
const port = 3000;

expressJSDocSwagger(app)(options);
```

- `Security` 关键字用于定义你的安全模式, 如果你不需要定义任何的安全模式，你可以忽略此项。

在添加安全模式之后,你可以在你的网络端点中使用它:

```javascript
/**
 * GET /api/v1
 * @summary This is the summary or description of the endpoint
 * @return {string} 200 - success response
 * @security BasicAuth
 */
app.get("/api/v1", (req, res) => res.send("Hello World!"));
```

swagger UI 界面会像下图所示:

<img src="./assets/security.png"/>

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/security/basic-auth.js)你可以参考更多的实例。
