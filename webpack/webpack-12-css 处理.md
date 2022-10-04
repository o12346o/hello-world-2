# css 处理

## 提取 css 文件

---

css 文件打包到 js 文件中，当 js 加载时，会创建一个 style 标签来生成样式。

对于网页而言，用户体验不好，会出现闪屏现象。

应该使用单独的 css 文件，通过 link 标签加载，提升性能。

### 1、下载包

```powershell
npm i mini-css-extract-plugin -D
```

### 2、配置

webpack.prod.js

```js
+ const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {  
  module:{  
   rules: [
      {
        test: /\.css$/,
        use: [
+          MiniCssExtractPlugin.loader,  // 将 css 提取成单独的文件
          'css-loader'
        ]
      }, 
    ]
  },
  plugins: [
+    new MiniCssExtractPlugin({
+      filename: "static/css/main.css"
    })
  ],
}
```

## css 兼容性处理

---

### 1、下载包

```powershell
npm i postcss-loader postcss postcss-preset-env -D
```

### 2、配置

webpack.prod.js

```js
{
        test: /\.less$/,
        use: [
          MiniCssExtractPlugin.loader, 
          'css-loader',
+          { // 兼容性问题处理在css-loader前面，less-loader后面
+            loader: "postcss-loader",
+            options: {
+              postcssOptions: {
+                plugins: [
+                  "postcss-preset-env", // 能解决大多数样式兼容性问题
+               ]
+              }
+           }
          },
          'less-loader'
        ]
      },
```

### 3、设定要兼容的浏览器版本

package.json

```json
"browserslist": [
    "last 2 version",
    "> 1%",
    "not dead"
]
```

最终设定取交集，即满足所有条件的浏览器版本。

## 封装样式 loader 函数

---

webpack.prod.js

```js
function getStyleLoader(pre) { // 样式 loader 函数
  return [
    MiniCssExtractPlugin.loader,  // 将 css 提取成单独的文件
    'css-loader',
    {
      loader: "postcss-loader",
        options: {
          postcssOptions: {
            plugins: [
              "postcss-preset-env", // 能解决大多数样式兼容性问题
            ]
          }
       }
    },
    pre
  ].filter(Boolean); // 当pre为空时，filter会过滤掉它。
}

module.exports = {
    module: {
        rules: [
            {
                test: /\.css$/,
                use: getStyleLoader() // 使用样式 loader 函数
            },
            {
                test: /\.less$/,
                use: getStyleLoader("less-loader") // 使用样式 loader 函数
            }
        ]
    }
}
```

## 压缩 css

---

### 1、下载包

```powershell
npm install css-minimizer-webpack-plugin --save-dev
```

### 2、配置

webpack.prod.js

```js
const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");

module.exports = {
  plugins: [
    new CssMinimizerPlugin()
  ],
}
```

最终，将会对打包后的css文件进行压缩。
