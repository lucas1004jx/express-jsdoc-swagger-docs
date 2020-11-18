# 复合模式
如果需要组合不同的模式,你可以参考[Swagger](https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not/), 使用express-jsdoc-swagger的接口, 你可以添加以下注释:

```javascript
/**
 * 一首歌
 * @typedef {object} IntrumentalSong
 * @property {string} title.required - 歌名
 * @property {string} band - 乐队
 * @property {number} year - 年份 - double
 */

/**
 * 一首歌
 * @typedef {object} PopSong
 * @property {string} title.required - 歌名
 * @property {string} artist - 歌手
 * @property {integer} year - 年份 - int64
 */

/**
 * GET /api/v1
 * @return {oneOf|IntrumentalSong|PopSong} 200 - 连接成功 - application/json
 */
```
在以上的例子中, 你可以发现我们使用了 “oneOf” 和两个模式来作为我们连接成功后的返回数据。

**需要注意的地方**是第一个值必须是条件，之后用`|`把每个模式分开，像这样：
```
{<条件>|<模式1>|...|<模式2>}

{oneOf|IntrumentalSong|PopSong}
```

目前我们支持, `oneOf`, `anyOf` 和 `allOf`.

> 你可以通过swagger.json来扩展其他使用, 请参考[扩展你的swagger文件](merge.md)来获取更多信息。

> 学习如何定义元件模式, 请参考[组件 / 模式](components.md)。

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/combineSchemas/index.js)有更多的参考例子.
