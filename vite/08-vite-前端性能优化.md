# vite 性能优化

- 开发时的构建速度优化
  
  - webpack 在这方面下的功夫是很重的：cache-loader  cache loader，（如果两次构建源代码没有产生变化，则直接使用缓存，不调用loader），thread-loader，开启多线程去构建...
  - vite 是按需加载，所有我们不太需要care这方面

- 页面性能指标：和我们怎么写代码有关
  
  - 首屏渲染时：fcp(firt content paint)，(first content paint，页面中第一个元素的渲染时长)
    - 懒加载：需要我们写代码实现
    - http优化：协商缓存、强缓存
      - 强缓存：服务器给响应头追加一些字段（expires），客户端会记住这些字段，在 expires（戒指失效时间）没有到达之前，无论你怎么刷新页面，浏览器都不会重新请求页面，而实从缓存里取
      - 协商 缓存：是否使用缓存要和后端商量一下，当服务器给我们打上协商缓存的标记后，客户端在下次刷新页面需要重新请求资源时会法送到一个协商请求给服务器，服务端如果说需要变化，则会响应具体的内容，如果服务器觉得没变化会响应304
  - 页面中最大元素的一个时长：lcp(largest content paint)
  - ...
  - js 逻辑也会影响性能：
    - 要注意副作用的清楚，组件会频繁的挂载和卸载，如果我们在卸载时不清除计时器，下次再次挂载时，计时器开了两个线程
    - 在写法上的一个注意事项：requestAnimationFram, requestIdleCallback，卡浏览器的帧率，对浏览器渲染原理要有一定的认识，然后在这方面优化
      - requestIdleCallback：传一个函数进去
      - 浏览器的帧率：16.6ms去更新一次（执行js逻辑 以及 重排重绘...），假设js执行逻辑超过了16.6，掉帧了
  - css
    - 关注继承属性：能继承的不要重复写
    - 尽量避免太过于深的css
  - 构建优化
    - 优化体积：压缩、treeshaking、图片资源压缩、cdn加载、分包、...

# 分包策略

**浏览器的缓存策略**

- 静态资源，名字没有变化，就不会重新去拿资源

- hash：只要内容有变化，hash字符串就完全不一样

**分包**就是将一些不会常规更新的内容（依赖的包）提取出来单独打包。

# gzip压缩

服务端：压缩文件

客户端：收到压缩包，解压缩

# 动态导入

动态导入 和 按需加载 是异曲同工的。

动态导入 是 es6 的一个新特性。

在路由中常用动态导入组件。

# cdn加速

**cdn**：内容分发网络（content delivery network）。

将我们依赖的第三方模块全部写成 cdn 的形式，然后保证我们自己代码的一个小体积（体积小服务器和客户端传输的压力就没那么大）。

## 安装插件

```bnf
npm i vite-plugin-cdn-import
```

## 使用插件

vite.config.js文件中

```js
import {defineconfig} from "vite"
import viteCDNPlugin from "vite-plugin-cdn-import"

export default defineconfig({
    plugins: [
        viteCDNPlugin({
             modules: [
                {   
                    name: "lodash",
                    var: "_",
                    path: "https://cdn.jsdeliver.net/npm/lodash@4.12.21/lodash.min.js"
                }
            ]
        })
    ]
})
```

main.js文件中

```js
import _ from "lodash"

const obj = _.deepClone({})

console.log("obj", obj) 
```
