# 实例

你可以使用`@example`标识符，并参考[swagger 文档](https://github.com/BRIKEV/express-jsdoc-swagger)为你的接口添加[例子](https://swagger.io/docs/specification/adding-examples/)。

以下的例子很清楚的描述了网络请求主体的信息，以及接口会返回怎样的状态。

```javascript
/**
 * POST /api/v1/song
 * @param {Song} request.body.required - Song info
 * @return {object} 200 - Success response
 * @return {object} 400 - Bad request response
 * @example request - example payload
 * {
 *   "title": "Bury The Light",
 *   "artist": "Casey Edwards ft. Victor Borba",
 *   "year": 2020
 * }
 * @example request - other payload example
 * {
 *   "title": "The war we made",
 *   "artist": "Red",
 *   "year": 2020
 * }
 * @example response - 200 - example success response
 * {
 *   "message": "You have added a song!"
 * }
 * @example response - 400 - example error response
 * {
 *   "message": "Failed to save song because you did not specify a title",
 *   "errCode": "EV121"
 * }
 */
app.post("/api/v1/song", (req, res) =>
  res.send({
    message: "You have added a song!",
  })
);
```

这个例子在 Swagger 界面中看起来会像这样：

<img src="./assets/examples.png"/>

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/requestBody/withExamples.js)或者[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/responses/withExamples.js)你可以查看更多的例子。

## 使用说明

`@example` 标记符后必须紧跟一个与该例子相关的关键词，例如“网络请求”或者“网络回复”。

> 不管是“网络请求”或者“网络回复”，你可以无限地添加例子，没有数量限制。如果是“网络回复”的例子，你也可以同时为同一个状态代码添加不同的例子。例如，我们可以为 API 成功返回后的数据添加不同的例子。

接下来的例子将会更详细的解释在各种不同的情况下（网络请求和网络回复）如何使用`@example`标识符。虽然大多数情况下都用法都差不多，但是根据关键词的不同，还是会有稍许的差异。

### 网络请求主体实例

```
@example 网络请求 - [概述]
[主体内容]
```

| 类别 | 描述 |
| --- | --- |                                                                     
| 概述 | 用简短的语句对例子做描述。所有的描述语句只能跟`@example`在同一行，换行后的部分将会归为主体内容部分。 |

| 主体内容 | 网络请求主体的主体内容实例。这部分内容不能与`@example`在同一行。必须写在`@example`的下一行。为了增加可读性，内容部分可以由多行组成。所有的断行，字间距都会在 Swagger UI 里表现出来。|

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/requestBody/withExamples.js)你可以查看更多的例子。

### 网络回复主体实例

```
@example response - [状态代码] - [概述]
[主体内容]
```

| 类别 | 描述 |
| --- | --- |
| 状态代码 | HTTP 转台代码 (例如: `200`). 请注意，只有在 [validStatusCodes](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/transforms/paths/validStatusCodes.js) 的代码才有有效. 同时, 必须要由 `@return` 标签，你的例子才会出现在 Swagger 的 UI 中。|
| 概述 | 用简短的语句对例子做描述。所有的描述语句只能跟`@example`在同一行，换行后的部分将会归为主体内容部分。 |
| 主体内容 | 网络回复主体的主体内容实例。这部分内容不能与`@example`在同一行。必须写在`@example`的下一行。为了增加可读性，内容部分可以由多行组成。所有的断行，字间距都会在 Swagger UI 里表现出来。 |

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/responses/withExamples.js)你可以查看更多的例子。
