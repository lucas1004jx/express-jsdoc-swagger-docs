# 网络请求主体

如果你需要使用 express-jsdoc-swagger 为网络端点添加[请求主体](https://swagger.io/docs/specification/describing-request-body/) 你可以添加以下的注释:

```javascript
/**
 * POST /api/v1/album
 * @param {object} request.body.required - songs info - application/json
 */
app.post("/api/v1/album", (req, res) => res.send("你成功保存了一首歌！"));
```

注解:

- `@param` 用来定义一个参数。
- [数据类型](https://swagger.io/specification/#data-types) 定义在 `{}`之间.
- 在数据类型之后, 你可以用关键字 **request.body**来表示这是一个网络请求主体。
- 在 `-`之间的部分是对参数的概述。
- 参数 `@param`的最后一部分 _(application/json)_ 用来阐明请求的类型。这部分不是必须的，默认值是 _application/json_。

你可以与 [组件](components.md) 结合，来写出相关的请求主体，如下列所示:

```javascript
/**
 * A song
 * @typedef {object} Song
 * @property {string} title.required - The title
 * @property {string} artist - The artist
 * @property {integer} year - The year - int64
 */

/**
 * POST /api/v1/song
 * @param {Song} request.body.required - song info
 * @return {object} 200 - song response
 */
app.post("/api/v1/songs", (req, res) => res.send("你成功保存了一首歌！"));

/**
 * POST /api/v1/album
 * @param {array<Song>} request.body.required - songs info
 * @return {object} 200 - album response
 */
app.post("/api/v1/album", (req, res) => res.send("你成功保存了一首歌！"));
```

或者你可以添加数据表格类型来上传文件:

```javascript
/**
 * A song
 * @typedef {object} Song
 * @property {string} title.required - The title
 * @property {string} artist - The artist
 * @property {string} cover - image cover - binary
 * @property {integer} year - The year - int64
 */

/**
 * POST /api/v1/album
 * @param {Song} request.body.required - songs info - multipart/form-data
 * @return {object} 200 - Album created
 */
app.post("/api/v1/album", (req, res) => res.send("你成功保存了一首歌！"));
```

在上例中, 在 `@param`的最后一部分，我们使用 multipart/form-data 来定义请求主体的类型。

swagger UI 界面会像下图所示:

<img src="./assets/request-body.png"/>

> 请参考[实例](examples.md) 来了解更多如何添加网络请求主体。

> 请参考[组件](components.md)来了解更多如何定义组件.

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/tree/master/examples/requestBody)你可以参考更多的例子。

### 请求主体作为表格参数

你可以不通过组件来传递参数，参考以下例子:

```javascript
/**
 * POST /api/v1/song
 * @param {string} id.form.required - This is the song id - application/x-www-form-urlencoded
 * @param {string} title.form.required - This is the song title - application/x-www-form-urlencoded
 * @return {object} 200 - song response
 */
app.post("/api/v1/songs", (req, res) => res.json({}));
```

注解:

- `@param` 用来定义一个参数。
- [数据类型](https://swagger.io/specification/#data-types) 定义在 `{}`之间.
- 在数据类型之后, 你可以在**form**之后定义参数关键字。
- 在 `-`之间的部分是对参数的概述。
- 参数 `@param`的最后一部分 _(application/json)_ 用来阐明请求的类型。这部分不是必须的，默认值是 _application/json_。

**注意:** 如果使用表格参数，需要为每一项提供概述

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/requestBody/formParameters.js)你可以参考更多的例子。
