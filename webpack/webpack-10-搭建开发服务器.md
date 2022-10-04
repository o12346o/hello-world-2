# 开发服务器&自动化

每次写完代码后，都需要手动输入指令才能编译代码，通过使用开发服务器，自动执行编译。

## 1、下载包

```js
npm install --save-dev webpack-dev-server
```

## 2、配置

webpack.config.js 文件中

```js
// 开发服务器
  devServer: {
    host: "localhost", // 服务器域名
    port: "3000", // 端口号
    open: true // 自动在浏览器中打开
  }
```

## 3、运行开发服务器

```powershell
npx webpack serve
```

开启服务器后，当源码改变时，自动更新打包。


