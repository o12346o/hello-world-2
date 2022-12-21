# vite 加载静态资源

什么是静态资源？

- 前端： 图片、视频资源等。

- 后端：除了动态 API，百分之九十九都视作静态资源。

## vite 对静态资源的处理

vite 中说的静态资源是前端静态资源。

vite 对静态资源是开箱即用的。

例如，引入 img 图像时：

```js
import imgURL from "./assets/img/01.jpg"

const img = document.createElement("img")
img.src = imgURL
document.body.appendChild(img)
```

其中，使用不同的参数，vite 会对资源做出不同的处理：

```js
// 引入 img 文件的 url 地址
import imgURL from "./assets/img/01.jpg" 

// 引入 img 文件的 url 地址
import imgURL from "./assets/img/01.jpg?url" 

// 引入 img 文件的 源码
import imgURL from "./assets/img/01.jpg?raw" 

// 引入 img 文件的 base64 格式代码
import imgURL from "./assets/img/01.jpg?base64" 

// 引入 svg 文件，通过这种方式直接将代码引入，减少 http 请求次数
import imgURL from "./assets/svg/fullscreen.svg?raw" 
```

> svg：scalable vector graphics 可伸缩矢量图形

## 别名

vite.config.js文件中：

```js
import { defineConfig } from "vite"
import path from "path"

export default defineConfig({
    resolve: {
        alias: {
            "@": path.resolve(__dirname, "./src"),
             "@assets": path.resolve(__dirname, "./src/assets")
        }
    }

})
```

### resolve.alias 原理

服务器端 对字符串进行处理，进行字符串替换，将 别名路径 转换为 绝对路径 。

服务器端 index.js 文件中：

```js
const Koa = require("koa") // 引入服务器框架 koa
const fs = require("fs")
cosnt path = require("path")

const viteConfig = require("./vite.config.js") // 引入 vite 配置文件
const aliasResolver = require("./aliasResolver.js") // 引入处理函数

const app = new Koa()

app.use(async (ctx) => { //context 上下文，包含：请求信息 响应信息
    console.log("ctx", ctx.request, ctx.response)
    // 通常使用中间件帮我们读文件即可，以下为自己读文件的方式
    if(ctx.request.url === "/"){
        const indexContent = await fs.promises.readFile(path.resolve(__dirname, "./index.html"))
        ctx.response.body = indexContent
        ctx.response.set("Content-type", "text/html")
    }
    if(ctx.request.url.endsWith(".js")){
        const jsContent = await fs.promises.readFile(path.resolve(__dirname, "." + ctx.request.url))
        // 处理 js 文件
        const result = aliasResolver(viteConfig.resolve.alias, jsContent)
       // 处理完成后
        ctx.response.body = result
        ctx.response.set("Content-type", "text/javascript")        
    }


})

app.listen(3000)
```

处理函数 aliasResolver.js 文件：

```js
module.exports = function aliasResolver(aliasConfig, jsContent){
    const entires = Object.entires(aliasConfig)
    console.log("entries", entries, jsContent)
    let result = jsContent
    entires.forEach(entire => {
        const {alia, path} = entire
        const srcIndex = path.indexOf("/src")
        const realPath = path.slice(srcIndex, path.length)
        result = jsContent.replace(alia, realPath)
    })
    return result
}
```

## vite 配置文件中对静态资源在生产环境的处理

打包后的静态资源为什么有 hash？

浏览器有一个缓存机制，静态资源只要名字不改，就会直接使用缓存。

刷新页面：请求的名字是不是同一个，来决定是否读取缓存

所以，我们要尽量避免名字一致

hash 算法：将一串字符串经过运算得到一个新的乱码字符串。只要文件内容变化，得到的 hash 值就会改变，通过 hash 告诉浏览器，是否使用缓存。。

> uuid ：全世界独一无二的。

vite.config.js 文件中：

```js
export default defineConfig({
    resolve:{
        alias: {}
    },
    optimizeDeps: {
        exclude: [],
    },
    envPrefix: "ENV_",
    css: {
    },
    build: { // 构建生成包时的一些策略
        rollupOptions: { // 配置 rollup 的一些构建策略
            output: { // 控制输出
                  // 在 rollup 里面，hash 代表将你的文件名和文件内容进行组合计算得到的结果。
                  assetFileNames: "[hash].[name].[ext]"
            }
        },
        assetsInlineLimit: 409600,  // 400kb，当小于该尺寸时，会将资源转为 base64 格式
       outDir: "dist",  // 配置输出目录
       assetDir: "static" // 配置输出目录中的静态资源目录
    }
})
```
