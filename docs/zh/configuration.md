# 配置

在开始使用前，你需要创建一个包含以下选项的配置文件:

- [基本信息](configuration.md?id=info)
- [服务器](configuration.md?id=servers)
- [安全](configuration.md?id=security)
- [文件路径](configuration.md?id=filespattern)
- [文件夹路径](configuration.md?id=basedir)

## 基本信息

The info options is the same as swagger specifies in [their documentation](https://swagger.io/specification/#info-object). It provides metadata about the API.

#### 基本信息选项实例

```javascript
{
  "title": "Sample Pet Store App",
  "description": "This is a sample server for a pet store.",
  "termsOfService": "http://example.com/terms/",
  "contact": {
    "name": "API Support",
    "url": "http://www.example.com/support",
    "email": "support@example.com"
  },
  "license": {
    "name": "Apache 2.0",
    "url": "https://www.apache.org/licenses/LICENSE-2.0.html"
  },
  "version": "1.0.1"
}
```

## 服务器

服务器的选项跟swagger[文档](https://swagger.io/specification/#server-object)中的一样，是一个服务器对象数组，用来为目标服务器提供连接信息。
#### 服务器选项实例

```javascript
{
  "servers": [
    {
      "url": "https://development.gigantic-server.com/v1",
      "description": "Development server"
    },
    {
      "url": "https://staging.gigantic-server.com/v1",
      "description": "Staging server"
    },
    {
      "url": "https://api.gigantic-server.com/v1",
      "description": "Production server"
    }
  ]
}
```

## 安全

安全设置选项请参考[swagger文档](https://swagger.io/specification/#security-requirement-object). 包含在API使用过程中哪些安全机制和安全配置可以被使用。

#### 安全配置实例

```javascript
{
  "security": {
    "BasicAuth": {
      "type": "http",
      "scheme": "basic"
    },
    "BearerAuth": {
      "type": "http",
      "scheme": "bearer"
    }
  }
}
```

## 文件路径

你可以配置文件路径给一个文件，或者给多个文件配置[全局路径](https://en.wikipedia.org/wiki/Glob_(programming))。

#### 文件路径配置实例

```javascript
{
  "filesPattern": "./basic-auth.js"
}
```

```javascript
{
  "filesPattern": "./**/*-routes.js"
}
```

## 文件夹路径

项目文件夹的绝对路径

#### 文件夹路径配置实例

```javascript
{
  "baseDir": __dirname
}
```

## 完整实例

```javascript
const express = require('express');

const expressJSDocSwagger = require('express-jsdoc-swagger');

// This is a full set of options
// It is not neccesary to complete every option
const options = {
  info: {
    version: '1.0.0',
    title: 'Albums store',
    license: {
      name: 'MIT',
      url: 'http://example.com',
    },
    description: 'API desctiption',
    contact: {
      name: 'contact name',
      url: 'http://example.com',
      email: 'test@test.com',
    },
    termsOfService: 'http://example.com',
  },
  servers: [
    {
      url: 'https://{username}.gigantic-server.com:{port}/{basePath}',
      description: 'The production API server',
      variables: {
        username: {
          default: 'demo',
          description: 'this value is assigned by the service provider, in this example `gigantic-server.com`',
        },
        port: {
          enum: [
            '8443',
            '443',
          ],
          default: '8443',
        },
        basePath: {
          default: 'v2',
        },
      },
    },
  ],
  security: {
    BasicAuth: {
      type: 'http',
      scheme: 'basic',
    },
  },
  file: './main.js',
  baseDir: __dirname,
};

const app = express();
const port = 3000;

expressJSDocSwagger(app)(options);

/**
 * GET /api/v1
 * @summary 这里用来描述接口
 * @return {string} 200 - 连接成功
 */
app.get('/api/v1', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening at http://localhost:${port}`));
```



