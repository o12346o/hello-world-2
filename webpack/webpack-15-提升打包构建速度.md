# 提升打包构建速度

## HotModuleReplacement

---

### 为什么

在开发过程中修改了一个模块代码，webpack 默认会将所有模块全部重新打包编译，速度很慢。

所以需要在修改某个模块时，只有这个模块代码需要重新打包编译，其他模块不变，这样打包速度就能快很多。

### 是什么

HotModuleReplacement（HMR 热模块替换）：在程序运行中，添加或是删除模块，而无需重新加载整个页面。

### 怎么用

webpack.dev.js

```js
module.exports = {
  // 其他代码省略
  devServer: {
    host: "localhost",
    port: "3000",
    open: true,
    hot: true, //开启 HMR 功能
  },
}
```

## OneOf

---

### 为什么

打包时，每个文件都会经过所有的 loader 处理，虽然因为 `test` 正则实际并没有处理，但是所有 loader 都有过一遍。比较慢。

### 是什么

就是只能匹配一个 loader，剩下的就不匹配了。

### 怎么用

```js
 module: {
    // 其他代码省略
    rules: [
      {
+        // 每个文件只能被一个 loader 匹配处理
+        oneOf: [
+          {
+            test: /\.css$/,
+           use: ['style-loader', 'css-loader']
+          },
+          // 其他 loader 省略
+        ]
      }
    ]
  },
}
```

## Exclude/Include

---

### 为什么

开发时，需要使用第三方库或插件，所有文件都下载到 node_modules 中了，而这些文件不需要编译就可以直接使用，无需再做处理。

所有在对 js 文件处理时，需要排除 node_modules 中文件。

### 是什么

- include：包含，只处理 xxx 文件。

- exclude：排除，除了 xxx 文件，其他文件都要处理。

### 怎么用

```js
 module: {
    // 其他代码省略
    rules: [
      {
        // 每个文件只能被一个 loader 匹配处理
        oneOf: [
          {
            test: /\.js$/,
 +          include: path.resolve(__dirname, "src") //只处理 src 目录下的 js 文件
            loader: 'babel-loader',
          },
          // 其他 loader 省略
        ]
      }
    ]
  },
  plugins: [
    new ESLintPlugin({
      context: path.resolve(__dirname,'../src'),
+     exclude: "node_modules" // 排除 node_modules 目录下的文件
    })
  ],
}
```

exclude、include 使用一个即可。

## Cache

---

### 为什么

每次打包时，js 文件都要经过 Eslint 检查 和 Babel 编译，速度比较慢。

可以缓存之前的 Eslint 检查 和 Babel 编译结果，这样二次打包时速度就会更快。

### 是什么

对 Eslint 检查 和 Babel 编译结果 进行缓存。

### 怎么用

```js
 module: {
    // 其他代码省略
    rules: [
      {
        // 每个文件只能被一个 loader 匹配处理
        oneOf: [
          {
            test: /\.js$/,
            include: path.resolve(__dirname,'../src'), // 只处理 src 目录下的 js 文件
            use: {
              loader: 'babel-loader',
+              options: {
+               cacheDirectory: true, // 开启 babel 缓存
+               cacheCompression: false // 关闭缓存文件压缩
+              }
            }
          }
          // 其他 loader 省略
        ]
      }
    ]
  },
  plugins: [
    new ESLintPlugin({
      context: path.resolve(__dirname,'../src'),
      exclude: "node_modules", // 排除 node_modules 目录下的文件
 +    cache: true, // 开启缓存
 +    cacheLocation: path.resolve(__dirname, '../node_modules/.cache/eslintcache')
    })
  ],
}
```

## Thead（多进程）

---

### 为什么

当项目越来越大时，打包速度越来越慢。

要提升打包速度，其实就是要提升 js 的打包速度（其他文件较少）。

对 js 文件处理主要时 eslint、Babel、terser 三个工具，所以我们要提升它们的运行速度。

可以开启多进程处理 js 文件，这样速度就比单进程打包更快了。

### 是什么

多进程打包：开启电脑的多个进程同时干一件事，速度更快。

注意：仅在特别耗时的操作中使用，因为每个进程启动就有大约 600ms 左右开销。

### 怎么用

启动进程的数量时 CPU 的核数-1。

1、如何获取 CPU 的核数：

```js
// node 核心模块，直接使用即可
const os = require('os');
// cpu 核数
const threads = os.cpus().length;
```

2、下载包

```powershell
npm i thread-loader -D
```

3、使用

```js
+ const os = require("os");
+ const TerserWebpackPlugin = require('terser-webpack-plugin'); // 压缩 js

+ const threads = os.cpus().length - 1; // 获取 cpu 核数，然后-1


module.exports = {  
  module: {
    rules: [
     {
      oneOf: [
        {
          test: /\.js$/,
          include: path.resolve(__dirname,'../src'), 
          use: [
+           {
+              loader: "thread-loader", // 开启多进程
+              options: {
+                works: threads, // 进程数量
+              }
+            },
            {
              loader: 'babel-loader',
              options: {
                cacheDirectory: true, 
                cacheCompression: false
              }
            }
          ]
        }
      ]
     }
    ]
  },
  // 4、插件
  plugins: [
    new ESLintPlugin({
      context: path.resolve(__dirname,'../src'),
      exclude: "node_modules",
      cache: true,
      cacheLocation: path.resolve(__dirname, '../node_modules/.cache/eslintcache'),
+     threads, // 使用多线程
    }),
  ],
+  optimization: {
+    // webpack5 压缩处理
+    minimizer: [
+      new CssMinimizerPlugin(),
+      new TerserWebpackPlugin({ // 压缩 js
+        parallel: threads,
+      })
+    ]
+  },
}
```
