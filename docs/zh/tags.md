# 标签

你可以为每个网络端点定义一系列的[标签](https://swagger.io/docs/specification/grouping-operations-with-tags/)。

通过 express-jsdoc-swagger 来定义标签:

```javascript
/**
 * GET /api/v1/album
 * @tags Album - everything about album
 */
```

注解:

- 关键字 `@tags` 用于标注网络端点。
- 被`-`隔开的部分是描述性语句。

此外, 同一个标签可以同时为几个不同的网络端点做标注:

```javascript
/**
 * GET /api/v1/songs
 * @tags Album
 * @tags Songs - everything about songs
 */
```

在上例中, `Album` 和 `Song` 标签同时标注了同一个网络端点, swagger UI 界面会像下图所示:

<img src="./assets/tags.png"/>

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/tree/master/examples/tags)你可以参考更多的实例。
