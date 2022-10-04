# 生产模式

生产模式是开发完成代码后，需要得到代码将来部署上线。

生产模式下，我们主要对代码进行优化让其运行性能更好。

优化主要从两个角度出发：

1. 优化待遇运行性能

2. 优化代码打包速度

## 生产模式准备

准备两个配置文件分别存放`开发模式`和`生产模式`的配置。

- `config/webpack.dev.js`

- `config/webpack.prod.js`

### 1、修改 webpack.dev.js

```js
const path = require("path"); // 用于解决路径问题
const HtmlWebpackPlugin = require('html-webpack-plugin');
const ESLintPlugin = require('eslint-webpack-plugin');

module.exports = {  
  entry: "./src/main.js",
  output: {
    path: undefined, // 开发模式无输出
    filename: "main.js",
},
  module: {
    rules: [
      // 代码省略显示
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      // 要修改路径
-     // template: path.resolve(__dirname, "public/index.html")
+      template: path.resolve(__dirname, "../public/index.html")
    }),
    new ESLintPlugin({
      // 要修改路径
      context: path.resolve(__dirname,'../src')
    })
  ],
  // 5、模式
  mode: "development",
  // 开发服务器
  devServer: {
    host: "localhost",
    port: "3000",
    open: true
  }
}
```

### 2、修改 webpack.prod.js

```js
const path = require("path"); // 用于解决路径问题
const HtmlWebpackPlugin = require('html-webpack-plugin');
const ESLintPlugin = require('eslint-webpack-plugin');

module.exports = {  
  entry: "./src/main.js",
  output: {
    path: path.resolve(__dirname, "../dist")
    filename: "main.js",
},
  module: {
    rules: [
      // 代码省略显示
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      // 要修改路径
-     // template: path.resolve(__dirname, "public/index.html")
+      template: path.resolve(__dirname, "../public/index.html")
    }),
    new ESLintPlugin({
      // 要修改路径
      context: path.resolve(__dirname,'../src')
    })
  ],
  // 5、模式
  mode: "production",
}
```

### 3、启动 开发模式 或 生产模式

启动开发模式

```powershell
npx webpack serve --config ./config/webpack.dev.js
```

启动生产模式

```js
npx webpack --config ./config/webpack.prod.js
```

### 3、修改 package.json

修改 package.json，使用脚本，来快捷启动。

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
+   "start": "npm run dev",
+   "dev": "webpack server --config ./config/webpack.dev.js",
+   "build": "webpack --config ./config/webpack.prod.js"
  },
```

**快捷启动开发模式：**

```powershell
npm start 
```

或

```powershell
npm run dev
```

**快捷启动生产模式：**

```powershell
npm run build
```
