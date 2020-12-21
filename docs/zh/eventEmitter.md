# 事件发生器

我们提供 [事件发生器](https://nodejs.org/api/events.html) 以便用户我们是如何解析注释和swagger 对象的。

用户可以监听以下的事件:

- **error** 在程序解析过程中，你可以监听该事件来调试程序。
- **process** 你可以监听该事件来查看jsdoc注释是如何解析成swagger对象的。
- **finish** 你可以监听该事件来查看swagger对象生成的结果。

## 实例

```javascript
  
const express = require('express');
const expressJSDocSwagger = require('express-jsdoc-swagger');

const options = {
  info: {
    version: '1.0.0',
    title: 'Albums store',
    license: {
      name: 'MIT',
    },
  },
  filesPattern: './simple.js',
  baseDir: __dirname,
};

const app = express();
const port = 3000;

const listener = expressJSDocSwagger(app)(options);

// Event emitter API
listener.on('error', error => {
  console.error(`Error: ${error}`);
});

listener.on('process', ({ entity, swaggerObject }) => {
  console.log(`entity: ${entity}`);
  console.log('swaggerObject');
  console.log(swaggerObject);
});

listener.on('finish', swaggerObject => {
  console.log('Finish');
  console.log(swaggerObject);
});

app.listen(port, () => console.log(`Example app listening at http://localhost:${port}`));
````

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/blob/master/examples/eventEmitter)你可以查看更多的例子

