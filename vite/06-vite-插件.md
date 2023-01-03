# vite 插件

插件是什么？

> vite 会在不同的生命周期的不同阶段中去调用不同的插件以达到不同的目的。

生命周期：vite 从开始执行到执行结束，整个过程就是 vite 的生命周期。

webpack 中插件举例：输出 html 文件(html-webpack-plugin)、清除输出目录（clean-webpack-plugin）

## 插件 vite-aliases

vite-aliases 可以帮我们自动生成别名：检测当前目录下包括 src 在内的所有文件夹，并帮助我们生成别名。

### 安装插件

```bash
npm i vite-aliases -D
```

### 使用插件

vite.config.js 文件中

```js
import {defineConfig} from "vite"
import {ViteAliases} from "vite-aliases"

export default defineConfig({
    plugins: [
        ViteAliases()
    ]
})
```

ViteAliases() 会帮我们自动生成别名：

```js
{
    “@”: "/src",
    "@assets": "/src/assets",
    ...
}
```

### 【原理】手写 vite-aliases 插件

插件就是在 vite 的生命周期的不同阶段去做不同的事情。

例如，vue 中的生命周期：created、mounted、...

我们去手写 vite-aliases 其实就是抢在 vite 执行配置文件之前去修改配置文件。

#### 定义插件

项目根目录 /plugins/ViteAliases.js 文件中

```js
// vite 的插件必须返回给 vite 一个配置对象
const fs = require("fs")
const path = require("path")

function diffDirAndFile(dirFilesArr = [], basePath = ""){ // 将路径中的文件夹路径提取出来的函数
    const result = {
        dirs: [],
        files: []
    }

    dirFilesArr.forEach(name => {
        const currentFileStat = fs.statSync(path.resolve(__dirname. basePath + "/" + name))
        console.log("current file stat", name, currentFileStat.isDirectory())
        const isDirectory = currentFileStat.isDirectory()

        if (isDirectory) {
            result.dirs.push(name)
        } else {
            result.files.push(name)
        }

    })

    return result
}

function getTotalSrcDir(keyName){ // 路径别名对象处理的函数
    const result = fs.readdirSync(path.resolve(__dirname, "../src"))
    console.log("result",result)
    const diffResult = diffDirAndFile(result,"../src")
    console.log("diffResult",diffResult)
    const resolveAliasesObj = {}
    diffResult.dirs.forEach(dirName => {
        const key = `${keyName}${dirName}`
        const absPath = path.resolve(__dirname, "../src" + "/" + dirName)
        resovleAliasesObj[key] = absPath
    })

    return resolveAliasesObj
}

export default ({
    keyName = "@"
} = {}) => {
    return {
        config(config, env) { 
            // config 函数可以返回一个对象，这个对象是部分的 viteConfig 配置
            // config: 目前的一个配置对象
            // env: mode: string, command: string
            // mode: development、production
            // command: serve、build
            console.log("config", config, env)
            // 通过调用函数，得到路径别名对象
            const resolveAliases = getTotalSrcDir(keyName)
            console.log("resolve", resolveAliases)
            return {
                // 在这里我们要返回一个 resolve 对象出去 
                resolve: {
                    alias: resolveAliases
                }
            }
        }
    }
}
```

#### 使用插件

vite.config.js 文件中：

```js
import {defineConfig} from "vite"
import {ViteAliases} from "vite-aliases"

import myViteAliases from "./plugins/ViteAliases"

export default defineConfig({
    plugins: [
        // ViteAliases(),
        myViteAliases()
    ]
})
```

vite 会对 vite.config.js 和 我们在插件 config 生命周期中返回的配置对象，进行合并处理。

## 插件 vite-plugin-html 及 vite-clean-clean

vite 内置非常多的插件，然后我们作为普通开发者不需要那么高的心智负担。

### 安装 vite-plugin-html 插件

```bash
npm i vite-plugin-html -D
```

### 使用 vite-plugin-html 插件

```js
import {createHtmlPlugin} from "vite-plugin-html"
export default defineConfig({
    plugins: [
        createHtmlPlugin({
            inject: {
                data: {
                    title: "首页" // 定义变量
                }
            }
        })
    ]
})
```

index.html 文件中，

使用 ejs 语法，使用 config 中定义的变量：

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><%= title %><title>
</head>
<body>
    <script src="./main.js" type="module"></script> 
</body>
</html>
```

### 【原理】手写create-html-plugin 插件

#### 定义插件

/plugins/CreateHtmlPlugin.js 文件中

```js
module.exports = (options) => {
    return {
        // 转换 html 的钩子
        transformIndexHtml:{
            enforce: "pre", // 将我们插件的一个执行时机提前
            transform: (html, ctx) => {
                // ctx 表示当前整个请求的一个执行上下文
                console.log("html",html)
                return html.replace(/<%= title %>/g, options.inject.data.title)
            }
        }
    }
}
```

#### 使用插件

vite.config.js 文件中

```js
import {defineConfig} from "vite"
import {ViteAliases} from "vite-aliases"

import myViteAliases from "./plugins/ViteAliases"
import myCreateHtmlPlugin from "./plugins/CreateHtmlPlugin"

export default defineConfig({
    plugins: [
        // ViteAliases(),
        myViteAliases(),
        myCreateHtmlPlugin({
            inject: {
                data: {
                    title: "主页2"
                }
            }
        })
    ]
})
```

## 插件 vite-plugin-mock

mock 数据：模拟数据。

前后端一般是并向开发：

- 后端：给出接口文档；

- 前端：mock数据，去做前端的工作。

前端怎么做？

1. 简单方式：直接去写死一两个数据，方便测试
   
   - 缺陷：
     - 没法做海量数据测试
     - 没法获取一些标准数据
     - 没法去感知http的异常

2. mockjs: 是用来模拟海量数据的，vite-plugin-mock 的依赖项就是mockjs

### 安装 vite-plugin-mock

```bash
npm i vite-plugin-mock mockjs -D
```

### 使用插件

```js
import {viteMockServe} from "vite-plugin-mock"

export default defineConfig({
    plugin: [
        viteMockServe({
            // default
            mockPath: 'mock',
            localEnabled: command === 'serve' 
        })
    ]
})
```

viteMockServe() 会自动查找文件 /src/mock/index.js ，文件中：

```js
// 设置简单模拟数据
const userList = [ 
    {
        name: "jack",
        age: 18,
        id: 1
    },
    {
        name: ""
    }
]

// 使用 mockjs 模拟数据
import mockJS from "mockjs"

const userList = mockJS.mock({
    "data|100":[{ // 表示生成 100 个data数据
        name: "@cname", // 表示生成不同的中文名
        “id|+1”: 1, // 表示生成不同的id，从1开始，每次+1
        time: "@time",
        date: "@date"
    }]
})

console.log("userlist", userList)

module.exports = [
    {
        method: "post",
        api: "api/users",
        response: ({ body }) => {
            // body，请求体
            return {
                code: 200,
                msg: "success",
                data: []
            } 
        }
    }
]
```

/src/main.js 文件中

```js
fetch("/api/users", {
    method: "post"
}).then(data => {
    console.log("data", data)
}).catch(error => {
    console.log("error", error)
})
```

### 【原理】手写 vite-plugin-mock

#### 定义插件

/plugins/VitePluginMock.js 文件中

```js
exposrt default (options) => { 
    // 做的最主要的事情就是拦截http请求
    // 例如，使用axios，会设置baseURL
    // 当打给本地服务器时， viteserver服务器接管
    return {
        congfigServer(server){
            // 服务器的相关配置
            const mockStat = fs.statSync("mock")
            const isDirectory  = mockStat.isDirectory()
            let mockResult = []
            if (isDirectory) {
                //process.cwd()，获取当前执行的根目录
                mockResult  = require(path.resolve(process.cwd(),"mock/index.js"))
                console.log("result", mockResult)
            }
            server.middelwares.use((req, res, next) => {
                // req, 请求对象
                // res, 响应对象
                // next(), 将处理结果交给下一个中间件
                console.log("req", req.url)
                // 检测我们请求的地址在 mockResult 里有没有
                const matchItem = mockResult.find(mockDescriiptor => mockDescriptor === req.usl)
                if(matchItem){
                    console.log("进来了")
                    const responseData = matchItem.response(req)
                    console.log("responseData", responseData)
                    // 强制设置一下请求头的格式为 json
                    res.end(JSON.stringify(responseData)) // 异步，设置请求头步
                } else {
                    next()  // 交给下一个中间件
                }
            })
        }
    }
}
```