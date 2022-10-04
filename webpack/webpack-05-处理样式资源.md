# 处理样式资源

使用 webpack 处理 css、less、sass、sytl 等样式资源。

## 介绍

---

webpack 本身不能识别样式资源，需要借助 loader 来帮助 webpack 解析样式资源。

[css-loader | webpack 中文网 (webpackjs.com)](https://www.webpackjs.com/loaders/css-loader/)

## 处理 css 资源

---

**1、下载包**

```powershell
npm i css-loader style-loader -D

# 等价于

npm install css-loader style-loader --save-dev
```

**2、功能介绍**

- `css-loader`：负责将 css 文件编译成 webpack 能识别的模块。

- `style-loader`：会创建一个 style 标签，里面放置 webpack 中 css 模块的内容。

此时，样式会以 style 标签的形式在页面上生效。

**3、配置**

webpack.config.js 文件中

```js
module: {
    rules: [
      // 使用 css-loader，处理 css 资源
      {
        test: /\.css$/,
        // loader: 'css-loader' // loader只能使用一个loader，use可以使用多个loader
        use: ['style-loader', 'css-loader']
      }
    ]
},
```

## 处理 less 资源

---

**1、下载包**

```powershell
npm i less-loader less -D
```

**2、功能介绍**

- `less-loader`：负责将 less 文件转换成 css 文件。

- `css-loader`：负责将 css 文件编译成 webpack 能识别的模块。

- `style-loader`：会创建一个 style 标签，里面放置 webpack 中 css 模块的内容。

**3、配置**

webpack.config.js 文件中

```js
module: {
    rules: [
      {
        test: /\.less$/,
        use: ['style-loader', 'css-loader', 'less-loader']
      }
    ]
  },
```

先使用 less-loader， 再使用 css-loader， 最后使用 style-loader。

## 处理 sass 资源

---

**1、下载包**

```powershell
npm i sass-loader node-sass -D
```

**2、功能介绍**

- `sass-loader`：负责将 less 文件转换成 css 文件。

- `css-loader`：负责将 css 文件编译成 webpack 能识别的模块。

- `style-loader`：会创建一个 style 标签，里面放置 webpack 中 css 模块的内容。

**3、配置**

webpack.config.js 文件中

```js
module: {
    rules: [
      {
        test: /\.s[ac]ss$/,
        use: ['style-loader', 'css-loader', 'sass-loader']
      }
    ]
  },
```

## 处理 sylus 资源

---

**1、下载包**

```powershell
npm i stylus-loader -D
```

**2、功能介绍**

- `sass-loader`：负责将 less 文件转换成 css 文件。

- `css-loader`：负责将 css 文件编译成 webpack 能识别的模块。

- `style-loader`：会创建一个 style 标签，里面放置 webpack 中 css 模块的内容。

**3、配置**

webpack.config.js 文件中

```js
module: {
    rules: [
      {
        test: /\.styl$/,
        use: ['style-loader', 'css-loader', 'stylus-loader']
      }
    ]
  },
```
