# webpack 基本使用

## 简介

**webpack** 是一个静态资源打包工具：

- 以一个或多个文件为打包的入口，将正项目文件编译组合成一个或多个文件输出。

- 输出的是编译好的文件，就可以在浏览器中运行了。

- 将 webpack 打包好的文件叫做 bundle。

---

## 功能介绍

webpack 本身的功能是有限的：

**开发模式**：仅能编译 js 中的 ES Module 语法。

**生产模式**：能编译 js 中的 ES Module 语法，还可以压缩 js 代码。

---

## 开始使用

### 1、资源目录

```
webpack_code    # 项目根目录
   └── src    # 项目源码目录
        ├── js    # js文件目录
        │    ├── count.js
        │    └── sum.js
        └── main.js    # 项目主文件
```

### 2、创建文件

创建 count.js 文件

```js
export default function count(x, y) {
    return x + y
}
```

创建 sum.js 文件

```js
export default function sum(...arr) {
    var res = 0
    arr.map(item => res += item)
    return res
}
```

创建 main.js 文件

```js
import {count} from 'count.js'
import {sum} from 'sum.js'


console.log(count(1,2))
console.log(sum(1,2,3,4))
```

### 3、下载依赖

初始化package.json  

```
npm init -y  
```

下载依赖  

```
npm install webpack webpack-cli -D
```

### 4、启用 webpack

**开发模式下启动**

```
npx webpack ./src/main.js --mode=development
```

**生产模式下启动**

```
npx webpack ./src/main.js --mode=production
```

**说明：**

- npx webpack 是用来运行本地安装 webpack 包的。

- ./src/main.js 是指定 main.js 文件开始打包，不仅会打包 main.js，还会将其依赖的文件都打包进来。

### 5、观察输出文件

打包文件默认在 dist 目录下，未设置 webpack.config.js 时，打包后的文件和入口文件同名。
