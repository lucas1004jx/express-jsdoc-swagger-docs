# 网络回复

如果你需要使用 express-jsdoc-swagger 为网络端点添加[网络回复](https://swagger.io/docs/specification/describing-responses/) 你可以添加以下的注释:

```javascript
/**
 * GET /api/v1
 * @summary 网络端点的概述
 * @return {string} 200 - 成功的回复
 * @return {object} 400 - 不成功的回复
 */
app.get("/api/v1", (req, res) => res.send("Hello World!"));
```

Where:

- `@summary` 是对端点的概述。
- `@return` 用对定义网络回复主体。
- [数据类型](https://swagger.io/specification/#data-types)定义在`{}`之间.
- 在数据类型之后, 你可以定义 HTTP 状态代码。
- 用`-`隔开的部分是对状态的描述。

你可以用`@deprecated`关键字来注明该端点已被弃用:

```javascript
/**
 * GET /api/v1/album
 * @summary 网络端点的概述
 * @deprecated
 * @return {object} 200 - 成功的回复
 * @return {object} 400 - 不成功的回复
 */
app.get("/api/v1/album", (req, res) =>
  res.json({
    title: "abum 1",
  })
);
```

如下图所示:

<img src="./assets/deprecated.png"/>

同时你也可以为每个 API 端点标记标签：

```javascript
/**
 * GET /api/v2/album
 * @summary 网络端点的概述
 * @tags album
 * @security BasicAuth
 * @return {object} 200 - 成功的回复
 * @return {object} 400 - 不成功的回复
 */
app.get("/api/v2/album", (req, res) =>
  res.json({
    title: "abum 1",
  })
);
```

> 如果你想了解更多 `@tags`, 请参考 [标签](tags.md)。

你可以返回回复主体:

```javascript
/**
 * GET /api/v1/albums
 * @summary 网络端点的概述
 * @tags album
 * @return {array<Song>} 200 - 成功的回复 - application/json
 */
app.get("/api/v1/albums", (req, res) =>
  res.json([
    {
      title: "abum 1",
    },
  ])
);
```

在上例中:

- 端点返回一个歌曲的数组
- 关键字 `@return`后的最后一个部分 _(application/json)_ 用来定义网络回复的类型，默认值是 _application/json_。

swagger UI 界面会像下图所示:

<img src="./assets/response-component.png"/>

> 请参考[实例](examples.md)来学习更多如何添加回复主体.

> 请参考[组件](components.md) 来学习更多如何定义组件模式.

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/tree/master/examples/responses)你可以参考更多的实例
