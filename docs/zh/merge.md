# 扩展 swagger 文件

如果你有项目已经使用了 swagger，你可以在 swagger 文件的基础上添加新的接口，或者添加一些我们不支持的新特性。

## 实例

你应该会有一个像这样的 `swagger.json` 文件:

<details><summary>点击看更多</summary>

```js
{
  "openapi": "3.0.0",
  "info": {
    "version": "1.0.0",
    "title": "Album store",
    "license": {
      "name": "MIT"
    }
  },
  "servers": [
    {
      "url": "http://example.com"
    }
  ],
  "tags": [
    {
      "name": "Songs",
      "description": "Everything about songs"
    }
  ],
  "paths": {
    "/songs": {
      "get": {
        "operationId": "songList",
        "tags": [
          "Songs"
        ],
        "responses": {
          "200": {
            "description": "songs array",
            "headers": {
              "x-next": {
                "description": "A link to the next page of responses",
                "schema": {
                  "type": "string"
                }
              }
            },
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Songs"
                }
              }
            }
          },
          "default": {
            "description": "unexpected error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            }
          }
        }
      },
      "post": {
        "summary": "Create a song",
        "security": [
          {
            "BasicAuth": []
          }
        ],
        "operationId": "createSong",
        "tags": [
          "Songs"
        ],
        "responses": {
          "201": {
            "description": "Null response"
          },
          "default": {
            "description": "unexpected error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            }
          }
        }
      }
    },
    "/song/{songId}": {
      "get": {
        "summary": "Info for a song",
        "operationId": "showSongById",
        "tags": [
          "Songs"
        ],
        "parameters": [
          {
            "name": "songId",
            "in": "path",
            "required": true,
            "description": "The id of the song to retrieve",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Expected response to a valid request",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Song"
                }
              }
            }
          },
          "default": {
            "description": "unexpected error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            }
          }
        }
      }
    }
  },
  "security": [
    {
      "BasicAuth": []
    },
    {
      "bearerAuth": []
    }
  ],
  "components": {
    "securitySchemes": {
      "BasicAuth": {
        "type": "http",
        "scheme": "basic"
      },
      "bearerAuth": {
        "type": "http",
        "scheme": "bearer",
        "bearerFormat": "JWT"
      }
    },
    "schemas": {
      "Song": {
        "type": "object",
        "required": [
          "id",
          "name"
        ],
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          }
        }
      },
      "Songs": {
        "type": "object",
        "properties": {
          "song": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Song"
            }
          }
        }
      },
      "Error": {
        "type": "object",
        "required": [
          "code",
          "message"
        ],
        "properties": {
          "code": {
            "type": "integer",
            "format": "int32"
          },
          "message": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

</details>

你的 SwaggerUI 会看起来像下图这样 I:

<img src="./assets/merge.png"/>

如果你想*整合*你的 `jsdoc`API 和`swagger.json`文件, 你可以参考下面的例子:

```javascript
const express = require("express");
const oldSwagger = require("./swagger.json"); //这是你之前的swagger.json文件
const expressJSDocSwagger = require("express-jsdoc-swagger");

const options = {
  info: {
    // 版本和标题是必须的
    version: "1.0.0",
    title: "Albums store",
  },
  filesPattern: "./simple.js",
  baseDir: __dirname,
};

const app = express();
const port = 3001;

// 第二个参数是之前的swagger.json文件:
expressJSDocSwagger(app)(options, oldSwagger);

// 新增接口例子:
/**
 * GET /api/v1/albums
 * @summary 对接口的概述
 * @tags 相册
 * @param {array<object>} name.query.required - 名字参数描述
 * @return {array<object>} 200 - 成功回复 - application/json
 */
app.get("/api/v1/albums", (req, res) =>
  res.json([
    {
      title: "abum 1",
    },
  ])
);

app.listen(port, () =>
  console.log(`Example app listening at http://localhost:${port}`)
);
```

最终, SwaggerUI 会像下图所示:

<img src="./assets/merge-result.png"/>

> 在[这里](https://github.com/BRIKEV/express-jsdoc-swagger/tree/master/examples/merge)你可以参考更多的例子
