# 组件
定义 `组件` [模式](https://swagger.io/docs/specification/components/):

```javascript
/**
 * 一首歌
 * @typedef {object} Song
 * @property {string} title.required - 歌名
 * @property {string} artist - 歌手
 * @property {number} year - 年份 - double
 */
```
模式解释:
- **typedef**是模式的名字而且是**required**（必须的）。
- 关键字 `@property` 用来定义属性.
- [数据类型](https://swagger.io/specification/#data-types) 需要定义在`{}`之间，之后紧跟属性的名字。
- 你可以通过定义`.required`来决定属性是否是必须的.
- 用` - `隔开的部分是其它非必须信息,例如对属性的描述格式.


```javascript
/**
 * 作者类型
 * @typedef {object} Author
 * @property {string} name.required - 作者名字
 * @property {integer} age - 作者年龄 - int64
 */
```

之间定义的两种模式(*歌和作者*)也可以用来作为其他模式的属性:
```javascript
/**
 * 歌辑
 * @typedef {object} Album
 * @property {Song} firstSong
 * @property {Author} author
 */
```

#### swagger UI 请参考以下图片:
<img src="./assets/components.png"/>

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/tree/master/examples/components)你可以参考更多的例子。
