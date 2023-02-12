# vue-cli 开发服务器代理配置

服务器代理：当客户端与服务器进行数据交互时，客户端浏览器有跨域限制；服务器与服务器进行数据交互，没有跨域限制。

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  lintOnSave: false,
  devServer: {
    proxy: { // 开发服务器代理配置
      '/api': { // 当匹配的 /api 时.向 目标服务器 取数据
        target: 'http://192.168.1.5:3000', // 指明目标服务器
        changeorign: true,
        pathRewrite: {
          '/api': '' // 重写url地址
        }
      }
    }
  }
})
```

服务器代理示意图：

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2023-02-13-00-53-11-image.png)
