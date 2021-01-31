# 参数

你可以使用以下的注解，通过 express-jsdoc-swagger，为你的服务端点添加[参数](https://swagger.io/docs/specification/describing-parameters/):

```javascript
/**
 * GET /api/v1/{id}
 * @summary 这是服务端点的概述
 * @param {string} name.query.required - 参数的描述
 * @param {number} id.path - 电话号码
 * @return {string} 200 - 回复成功
 */
app.get("/api/v1/:id", (req, res) => res.send("Hello World!"));
```

注解:

- `@param` 用于定义参数.
- [类型](https://swagger.io/specification/#data-types) 需要定义在 `{}`之间.
- 在定义类型之后, 你需要定义参数的名字。
- 具体如下:
  - `* @param {string} name.query.required` 这是个必须参数.
  - `* @param {string} name.query.deprecated` 表明该参数已不再使用
  - `* @param {string} name.query` 单纯的定义参数名字
- 在 `-`之后可以对参数做简短的描述.

你可以在参数后添加 **enum values**:

```javascript
/**
 * GET /api/v1/albums
 * @summary 这是服务端点的概述
 * @param {string} name.query.required - 参数的描述 - enum:type1,type2
 * @param {string} license.query - enum:MIT,ISC - 参数的描述
 * @return {object} 200 - 回复成功 - application/json
 */
```

最后一个参数可以用作枚举参数类型，参数的描述和枚举可以调换位置。

swagger UI 界面会像下图所示:

<img src="./assets/parameters.png"/>

> You can check out more examples [here](https://github.com/BRIKEV/express-jsdoc-swagger/tree/master/examples/parameters).
