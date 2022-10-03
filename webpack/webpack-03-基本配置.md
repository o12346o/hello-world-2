# webpack-03-基本配置

## 5大核心配置

---

**1、entry（入口）**

指明从哪个文件开始打包。

**2、output（输出）**

指明打包后的输出文件路径，文件名。

**3、module（加载器）**

webpack 本身只能处理 js、json 文件，需要导入 loader 后，才能处理其他文件。

**4、plugin（插件）**

扩展 webpack 的功能。

**5、mode（模式）**

主要有两种模式：

- 开发模式：development

- 生产模式：production



## 进行 webpack 配置

---

webpack.config.js文件中

```js
const path = require("path"); // 用于解决路径问题

module.exports = {  
  // 1、入口
  entry: "./src/main.js",
  // 2、输出
  output: {
    // 输出路径
    // __dirname，当前文件所处的文件夹路径
    // path.resolve()，用于连接路径
    path: path.resolve(__dirname,"dist"), //绝对路径
    // 输出文件名
    filename: "main.js",
  },
  // 3、加载器
  module: {
    rules: [

    ]
  },
  // 4、插件
  plugins: [

  ],
  // 5、模式
  mode: "production"
}
```

打包时，`npx webpack`，即可自动调用 webpack.config.js ，进行打包。






