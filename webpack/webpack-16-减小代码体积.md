# 减小代码体积

## Tree Shaking

---

### 为什么

开发时我们定义了一些工具函数库，或者引用第三方工具函数库或组件库。

如果没有特殊处理的话，打包时会引入整个库，但实际上可能只用了极小部分，这样将整个库都打包进来，体积就太大了。

### 是什么

`Tree Shaking` 是一个术语，通常用于描述移出 JavaScript 中没有使用的代码。

注意：它依赖 `ES Module` 。

### 怎么用

webpack 已经默认开启了这个功能，无需其他配置。

## Babel

---

### 为什么

babel 为编译的每个文件都插入了辅助代码，使代码体积过大。

babel 对一些公共方法使用了非常小的辅助代码，比如`_extend` 。默认情况下会被添加到每一个需要它的文件中。

可以将这些辅助代码作为一个独立模块，来避免重复引入。

### 是什么

`@babel/plugin-transform-runtime` ：禁用了 babel 自动对每个文件的 runtime 注入，而是引入`@babel/plugin-transform-runtime` 并且使得所有辅助代码从这里引用。

### 怎么用

1、下载包

```powershell
npm i @babel/plugin-transform-runtime
```

2、配置

```js
 {
     loader: 'babel-loader',
     options: {
         // presets: ['@babel/preset-env'], // @babel-preset-env 是插件预设
         cacheDirectory: true, // 开启 babel 缓存
         cacheCompression: false, // 关闭缓存文件压缩
+        plugins: ["@babel/plugin-transform-runtime"], // 减少代码体积
     }
}
```

## image Minimizer

---

### 为什么

项目中引用了较多的图片，图片体积会较大，将来请求速度较慢。

可以对图片进行压缩，减少图片体积。

注意：本地项目静态图片才需要进行压缩，在线图片不需要。

### 是什么

`image-minimizer-webpack-plugin` ：用来压缩图片的插件。  

### 怎么用

1、下载包

```powershell
npm i image-minimizer-webpack-plugin imagemin -D
```

还有以下包需要下载：

- 无损压缩

```powershell
npm install imagemin-gifsicle imagemin-jpegtran imagemin-optipng imagemin-svgo --save-devv
```

- 有损压缩

```powershell
npm install imagemin-gifsicle imagemin-mozjpeg imagemin-pngquant imagemin-svgo --save-dev
```

2、配置

```js
 const ImageMinimizerPlugin = require("image-minimizer-webpack-plugin");  // 压缩图片

 optimization: {
    minimizer: [
      // 压缩图片
      new ImageMinimizerPlugin({
        minimizer: {
          implementation: ImageMinimizerPlugin.imageminGenerate,
          options: {
            plugins: [
              ["gifsicle", { interlaced: true }],
              ["jpegtran", { progressive: true }],
              ["optipng", { optimizationLevel: 5 }],
              [
                "svgo",
                {
                  plugins: [
                    "preser-default",
                    "prefixIds",
                    {
                      name: "sortAttrs",
                      params: {
                        xmlnsOrder: "alphabettical",
                      }
                    }
                  ]
                }
              ]
            ],
          }
        },
      }),
    ],
 }
```
