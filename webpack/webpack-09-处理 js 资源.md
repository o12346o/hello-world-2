# 处理 js 资源

原因是 webpack 对 js 的处理有限，只能编译 js 中的 ES 模块化语法，不能编译其他语法，导致 js 不能在 IE 等浏览器运行，所以需要做一些兼容性处理。

其次，开发过程中，代码格式需要规范，需要工具来检查代码规范。

- 针对 js 兼容性处理，使用 babel 来完成。

- 针对代码格式，使用  Eslint 来完成。

## Eslint

---

检查 js 和 jsx 语法。

通过 Eslint 配置，设置规则，在运行 Eslint 时对代码进行检查。

### 1、配置文件

配置文件有多种写法，位于项目根目录：

- `.eslintrc`

- `.es lintrc.js`

- `.eslintrc.json`

- `package.json` 中 `eslintconfig` ：不需要创建文件，在原有文件基础上写，Eslint 会自动读取它们。

区别在于格式不同，只用一种接口。

### 2、具体配置

以 `.eslintrc.js` 配置文件为例：

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
  }
};
```

### 3、webpack.config.js 中注册 eslint 插件

首先， `npm i eslint eslint-webpack-plugin -D`安装依赖包。

然后，在 wenpack.config.js 中注册 eslint 插件。

```js
const ESLintPlugin = require('eslint-webpack-plugin');

module.exports = {
    plugins: [
        // 插件 导入位置
+        new ESLintPlugin({
+          context: path.resolve(__dirname,'src')
+        })
   ],
}
```

注：vscode 中使用 Eslint 插件，可以在写代码过程中进行提醒。

### 4、忽略文件

在项目根目录下创建 `.eslintignore`文件，在文件中指明要忽略哪些文件，被忽略的文件不做代码检查。

类似`.gitignore` 文件。

```
dist # 忽略打包后的 dist 文件
```

## Babel

---

JavaScript 编译器。

主要用于将 ES6 语法编写的代码转换为向后兼容的 JavaScript 语法，以便代码能运行在在浏览器及其他环境中。

### 1、配置文件

配置文件有多种写法，位于项目根目录：

- `babel.config.js`

- `babel.config.json`

- `.babelrc`

- `.babelrc.js`

- `babelre.json`

- `package.json` 中` babel` ：不用创建单独文件，在原文件基础上写，Babel 会自动读取。

区别在于格式不同，只需要一个即可。

### 2、具体配置

以 `babel.config.js` 配置文件为例：

```js
module.exports = {
  // 智能预设，能够编译 ES6 语法
  presets: ['@babel/preset-env']
};
```

### 3、webpack.config.js 中使用 babel-loader

首先， `npm install -D babel-loader @babel/core @babel/preset-env`安装依赖包。

然后，在 wenpack.config.js 中使用 babel-loader。

```js
{
      test: /\.js$/,
      exclude: /node_modules/, // 排除 node_modules 中的文件
      loader: 'babel-loader',
}
```

在使用 babel-loader 时，会自动查找 babel.config.js 中的配置并使用。

也可以使用 babel-loader 的同时进行配置。

```js
{
      test: /\.js$/，
      exclude: /node_modules/, // 排除 node_modules 中的文件
      loader: 'babel-loader',
      options: {
          presets: ['@babel/preset-env']
      }
}
```