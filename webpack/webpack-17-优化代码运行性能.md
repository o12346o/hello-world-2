# 优化代码运行性能

## Code Split

---

### 为什么

打包代码时，会将所有 js 文件打包到一个文件中，体积太大了。如果只渲染首页，就应该只加载首页的 js 文件，其他文件不应该加载。

所以，需要将打包生成的文件进行代码分割，生成多个 js 文件，渲染哪个页面就只加载某个 js 文件，这样加载的资源少，速度更快。

### 是什么

代码分割（Code Split）主要做了两件事：

1. 分割文件：将打包生成的文件进行分割，生成多个 js 文件。

2. 按需加载：需要哪个文件就加载哪个文件。 

### 怎么用

代码分割实现方式有多种：

#### 1、多入口

```js
 entry: {
    app: "./src/app.js",
    main: "./src/main.js",
 },
 output: {
    path: path.resolve(__dirname,"dist"), //绝对路径
    filename: "[name].js", // 使用 entry 中定义的名字
    clean: true // 清理旧版本文件
  },
```

#### 2、多入口提取公告模块

```js
optimization: {
    splitChunks: {
      chunks: "all", // 对所有模块都进行分割
      // 以下是默认值
      // minSize: 20000, //分割代码最小的大小
      // minRemainingSize: 0, // 最后提取的文件大小不能为 0
      // minChunks: 1, // 至少被引用的次数，满足条件才会被分割
      // maxAsyncRequests: 30, // 按需加载时并行加载的文件的最大数量
      // maxInitialRequests: 30, // 入口 js 文件最大并行请求数量
      // enforceSizeThreshold: 50000, // 超过 50kb 一定会单独打包（此时会忽略 minRemainingSize、 maxAsyncRequests、 maxInitialRequests）
      // cacheGroups: {
      //   // 组，哪些模块打包要到一个组
      //   defaultVendors: {
      //     test: /[\\/]node_module[\\/]/, // 需要打包到一起的模块
      //     priority: -10, //权重（越大越高）
      //     reuseExistingChunk: true, // 如果当前 chunk 包含已从主 bundle 中拆分出的模块，则它将被重用，而不是生成新的模块
      //   },
      //   default: { // 其他没有写的配置会使用上面的默认值
      //     miniSize: 0, // 这里的权重更大
      //     minChunks: 2,
      //     priority: -20,
      //     reuseExistingChunk: true,
      //   }
      // }
      // 修改配置
      cacheGroups: {
        // 组，哪些模块打包要到一个组
        defaultVendors: {
          test: /[\\/]node_module[\\/]/, // 需要打包到一起的模块
          priority: -10, //权重（越大越高）
          reuseExistingChunk: true, // 如果当前 chunk 包含已从主 bundle 中拆分出的模块，则它将被重用，而不是生成新的模块
        },
        default: {
          // 其他没有写的配置会使用上面的默认值
          minSize: 0,
          minChunks: 2,
          priority: -20,
          reuseExistingChunk: true,
        }
      }
    }
  }
```

#### 3、按需加载，动态导入

main.js 文件中：

```js
import sum from "./math" // 直接加载，静态导入

console.log('main');
console.log(sum(4,5,6));

document.getElementById("btn").onclick = function() {
  // 按需加载，动态导入
  import("./count")
    .then(res => {
      console.log("模块加载成功", res.default(1,2));
    })
    .catch(err => {
      console.log("模块加载失败", err);
    })
}
```

解决 import 报错问题，.eslintrc.js文件中：

```js
module.exports = {
  // 继承 Eslint 规则
  extends: ["eslint:recommended"],
  env: {
    node: true, // 启用 node 中全局变量
    browser: true, // 启用浏览器中全局变量
  },
  parserOptions: {
    ecmaVersion: 6, // es6
    sourceType: "module", // es module
  },
  rules: {
    "no-var": 2, // 不能使用 var 定义变量
  },
+ plugins: ["import"] // 解决 import 报错问题
};
```

#### 4、单入口

```js
entry:"./src/main.js",

optimization: {
    splitChunks: {
      chunks: "all", // 对所有模块都进行分割
      // 使用默认值即可
    }
}
```

#### 5、给动态导入文件命名

main.js 文件中：

```js
document.getElementById("btn").onclick = function() {
  // webpack 魔法命名 
  // /* webpackChunkName: "count" */ -- 这是 webpack 动态导入模块命名的方式
  // "count" 将来会作为 [name] 的值显示。
  import(/* webpackChunkName: "count" */ "./js/count")
    .then(res => {
      console.log("模块加载成功", res.default(1,2));
    })
    .catch(err => {
      console.log("模块加载失败", err);
    })
}
```

#### 6、统一命名

webpack.prod.js 和 webpack.dev.js 文件中：

```js
output: {
+    // 给打包输出的其他文件命名
+    chunkFilename: "static/js/[name].chunk.js",
+    // 图片、字体等通过 type:asset处理资源命名方式
+    assetModuleFilename: "static/media/[hash:10][ext][query]",
},


module: {
    rules: [
        oneOf: [
          {
              test: /\.(ttf|woff2?|mp3|mp4|avi)$/,
              type: "asset/resource",
-             // generator: { // 自定义输出目录
-             //     filename: 'static/medias/[hash:10][ext][query]' 
-             // }
          },
        ]
    ]
},


plugins: [
    new MiniCssExtractPlugin({
      // 将 css 提取成单独的文件,开发模式不起作用
      filename: "static/css/main.css",
+     chunkFilename: "static/css/[name].chunk.css",
    }),
]
```

## Preload/Prefetch

---

### 为什么

虽然使用 imp这样实现的ort 动态导入语法按需加载（也叫懒加载，路由懒加载也是这样实现的）。

但是加载速度仍有提升空间，例如，在用户点击时才加载，需要等待加载完成。

在浏览器空闲时间，加载后续需要使用的资源。就需要用 `preload` 或 `prefetch` 技术。

### 是什么

- `preload`: 告诉浏览器立即加载资源。

- `prefetch` : 告诉浏览器在空闲时加载资源。

它们的共同点：

- 都只会加载资源，并不执行。

- 都有缓存。

它们的区别：

- `preload` 加载优先级高，`prefetch` 加载优先级低。

- `preload` 只能加载当前页面需要的资源，`prefetch` 可以加载当前页面资源，也可以加载下一个页面需要的资源。

- `preload` 兼容性比 `prefetch` 好。

### 怎么用

#### 1、下载包

```powershell
npm install --save-dev @vue/preload-webpack-plugin
```

#### 2、配置

```js
const PreloadWebpackPlugin = require('@vue/preload-webpack-plugin');

plugins: [
  new HtmlWebpackPlugin(),
  new PreloadWebpackPlugin({
    //rel: 'preload',
    // as: 'script',
    rel: 'preretch'，
  })
]
```

## NetWork Cache

---

### 为什么

### 是什么

### 怎么用

1、所有文件名都加上 contenthash ，contenthash 会根据文件内容变化。当文件内容不变时，contenthash 不变。

```js
 new MiniCssExtractPlugin({ // 将 css 提取成单独的文件
      filename: "static/css/main.[contenthash:10].css",
      chunkFilename: "static/css/[name].chunk.[contenthash:10].css",
 }),
```

2、将运行时的 chunk 文件提取出来：

```js
optimization: [
    runtimeChunk: { // 运行时的chunk文件
      name: entrypoint => `runtime~${entrypoint.name}.js`
    }
]
```

设置 runtimeChunk 是将包含`chunks 映射关系`的 list单独从 main.js里提取出来，因为每一个 chunk 的 id 基本都是基于内容 hash 出来的，所以每次改动都会影响它，如果不将它提取出来的话，等于main.js每次都会改变。缓存就失效了。设置runtimeChunk之后，webpack就会生成一个个runtime~xxx.js的文件。  
然后每次更改所谓的运行时代码文件时，打包构建时main.js的hash值是不会改变的。如果每次项目更新都会更改main.js的hash值，那么用户端浏览器每次都需要重新加载变化的main.js，如果项目大切优化分包没做好的话会导致第一次加载很耗时，导致用户体验变差。现在设置了runtimeChunk，就解决了这样的问题。所以`这样做的目的是避免文件的频繁变更导致浏览器缓存失效，所以其是更好的利用缓存。提升用户体验。`

## Core.js

---

### 为什么

使用 babel  对 js 代码进行兼容性处理，其中使用 @babel/preset-env 智能预设来处理兼容性问题。它能将 es6 的一些语法进行编译转换。

但是 async 函数、promise 对象、数组的一些方法等，它没法处理。

js 代码仍然存在兼容性问题。

### 是什么

`core-js` 是专门用来做 es6 及以上 api 的 `polyfill` 。

`polyfill` 叫做垫片、补丁。就是用社区上提供的一段代码，在不兼容的浏览器上，使用该新特性。

### 怎么用

main.js 文件中使用 Promise ：

```js
new Promise((resolve) => {
    setTimeout(() => {
        resolve()
    },1000)
})
```

#### 1、下载包

```powershell
npm i core-js
```

#### 2、手动全部引入

main.js 文件中：

```js
import "core-js"
```

缺点：会引入全部兼容性代码，体积太大了。

#### 3、手动按需引入

main.js 文件中：

```js
import "core-js/es/promise"
```

#### 4、自动按需引入

main.js 文件中无需配置，在 babel.config.js 文件中：

```js
module.exports = {
    presets: [
        [
            "@babel/preset-env",
            {
                useBuiltIns: "usage", // 按需加载自动引入
                corejs: 3,
            }
        ],
    ],
}
```

## PWA

---

### 为什么

开发 web App 项目，项目一旦处于网络离线情况，就没法访问了。

希望给项目提供离线体验。

### 是什么

渐进式网路应用程序（progressive web application -PWA）：是一种可以提供类似于 native app（原生应用程序）体验的 web App 的技术。

其中最重要的是，在离线（offline）时程序能够继续运行功能。

内部通过 Service Workers 技术实现。

### 怎么用

#### 1、下载包

```powershell
npm i workbox-webpack-plugin -D
```

#### 2、修改配置文件

```js
const WorkboxPlugin = require("workbox-webpack-plugin");

module.exports = {
  plugins: [
    new WorkboxPlugin.GenerateSw({
      clientsClaim: true,
      skipWaiting: true,
    }),
  ],
}
```

#### 3、注册 service Worker

main.js 文件中：

```js
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js').then(registration => {
      console.log('SW registered: ', registration);
    }).catch(registrationError => {
      console.log('SW registration failed: ', registrationError);
    });
  });
}
```

#### 4、使用 service Worker

在脱机状态下，代码加载履行者是service Worker。
