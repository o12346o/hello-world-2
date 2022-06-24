# 1. 模块化的基本概念

1.1 什么是模块化

遵循固定的规则，把一个大文件拆成独立并相互依赖的多个小模块。

把代码进行模块化拆分的好处：

1. 提高了代码的复用性

2. 提高了代码的可维护性

3. 可以实现按需加载

## 1.2 模块化规范

模块化规范就是对代码进行模块化的拆分与组合时，需要遵守的规则。

例如：

- 使用什么样的语法格式来引用模块

- 在模块中使用什么样的语法格式向外暴露成员

模块化规范的好处：遵守统一的模块化规范，降低了沟通成本，方便了各个模块之间的相互调用。

# 2. Node.js 中模块化

## 2.1 Node.js 中模块的分类

根据来源的不同，将模块分为3大类：

- 内置模块（由 Node.js 官方提供）

- 自定义模块（用户创建的每个 js 文件，都是自定义模块）

- 第三方模块（由第三方开发的模块，使用前需要先下载）

## 2.2 加载模块

使用强大的 require() 方法，可以加载需要的内置模块、用户自定义模块、第三方模块。

```javascript
// 1.加载内置的 fs 模块
const fs = require('fs')
// 2.加载用户自定义模块
const custom = require('./custom.js')
// 3.加载第三方模块
const moment = require('moment')
```

## 2.3 Node.js 中的模块作用域

**1. 什么是模块作用域**

和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做模块作用域。

**2. 模块作用域的好处**

防止了全局污染的问题

## 2.4 向外共享模块作用域中的成员

### 1. module 对象

在每个 js 自定义模块中，都有一个 module 对象，它里面储存了和当前模块有关的信息。

```javascript
console.log(module)
```

打印结果：

```bash
Module {
  id: '.',
  path: 'D:\\website\\Node-2022-06-23',
  exports: {},
  filename: 'D:\\website\\Node-2022-06-23\\01 module 对象.js',
  loaded: false,
  children: [],
  paths: [
    'D:\\website\\Node-2022-06-23\\node_modules',
    'D:\\website\\node_modules',
    'D:\\node_modules'
  ]
}
```

### 2. module.exports 对象

在自定义模块中，可以使用 module.exports 对象，将模块中的成员共享出去，供外界使用。

自定义模块 01.js 中：

```javascript
// 在一个自定义模块中，默认情况下，module.exports = {}

// 向 module.exports 对象上挂载 username 属性
module.exports.username = 'jack'
// 向 module.exports 对象上挂载 sayHi 方法
module.exports.sayHi = function(){
    console.log('Hello!')
}
```

外界使用 require() 方法导入自定义模块是，得到的就是 module.exports 所指向的对象。

自定义模块 02.js 中：

```javascript
const m = require('./01.js')

console.log(m)
```

打印结果为：

```bash
{ username: 'jack', sayHi: [Function (anonymous)] }
```

### 3. 共享成员时的注意点

使用 require() 方法导入模块时，导入的结果，永远以 module.exports 指向的对象为准。

自定义模块 01.js 中：

```javascript
module.exports.usrname = 'jack'
module.exports.age = 18

// 创建一个全新的 module.exports 对象
module.exports = {
  nickname: 'tom',
  sayHi() {
    console.log('Hi！')
  }
}
```

自定义模块 02.js 中：

```javascript
const m = require('./01.js')

console.log(m)
```

打印结果为：

```bash
{ nickname: 'tom', sayHi: [Function: sayHi] }
```

### 4. exports 对象

为了简化代码，Node.js 提供了 exports 对象。默认情况下，exports 和 module.exports 指向同一个对象。最终共享的结果，还是以 module.exports 指向的对象为准。

### 5. exports 和 module.exports 的使用误区

时刻谨记，使用 require() 方法 导入模块时，得到的永远是 module.exports 指向的对象。

【例一】

```javascript
exports.username = 'jack'
module.exports = {
    gender: '男'，
    age: 20
}
```

module.exports 中：

```bash
{ gender: '男', age: 20 }
```

【例二】

```javascript
module.exports.username = 'jack'
exports = {
    gender: '男',
    age: 22
}
```

module.exports 中：

```bash
{ username: 'jack' }
```

【例三】

```javascript
exports.username = 'jack'
module.exports.age = 18
```

module.exports 中：

```bash
{ username: 'jack', age: 18 }
```

【例四】

```javascript
exports = {
  gender: '男',
  age: 22
}
module.exports = exports
module.exports.username = 'jack'
```

module.exports 中：

```bash
{ gender: '男', age: 22, username: 'jack' }
```

**注意：** 为了防止混乱，建议不要在同一个模块中同时使用 exports 和 module.exports ，只选用一种即可。

## 2.6 Node.js 中的模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。

CommonJS 规定：

- 每个块内部，module 变量代表当前模块。

- module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。

- 加载某个模块，其实是加载该模块的 module.exports 属性，require() 方法用于机制模块。

# 3. npm 与 包

## 3.1 包

### 1. 什么是包

Node.js 中的 *第三方模块* 又叫做 *包* 。

### 2. 包的来源

不同于 Node.js 中的内置模块和自定义模块，包是由第三方个人或团体开发出来的，免费供所有人使用。

注意：Node.js 中的包都是免费且开源的，不需要付费即可免费下载使用。

### 3. 为什么需要包

由于 Node.js 的内置模块仅仅提供了一些底层API，导致在基于内置模块进行项目开发时，效率很低。

包是基于内置模块封装出来的，提供了更高级、更方便的API，极大的提高了开发效率。

包和内置模块之间的关系，类似于 jQuery 和 浏览器内置API 之间的关系。

### 4. 从哪里下载包

从  https://www.npmjs.com/  搜索包。

从  https://registry.npmjs.org/  服务器上下载包。

### 5. 如何下载包

通过 npm 下载包。

npm包管理工具（ Node Package Manager），随着 Node.js 的安装一起装的了电脑上。

可以在终端执行 `npm -v` 查看已经安装的 npm 的版本号。

## 3.2 npm 初体验

### 1. 格式化时间的传统做法

1. 创建格式化时间的自定义模块
   
   1. 定义格式化时间的方法
   
   2. 创建补零函数
   
   3. 从自定义模块中导出格式化时间的函数

2. 导入格式化时间的自定义模块

3. 调用格式化时间的函数

**代码演示**

01.js文件中：

```javascript
// 创建格式化时间的自定义模块

// 1.定义格式化时间的方法
function dateFormat(dtStr){
  const dt = new Date(dtStr)

  const y = padZero(dt.getFullYear())
  const m = padZero(dt.getMonth() + 1)
  const d = padZero(dt.getDate())

  const hh = padZero(dt.getHours())
  const mm = padZero(dt.getMinutes())
  const ss = padZero(dt.getSeconds())

  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}
// 2.创建补零函数
function padZero(n){
  return n > 9 ? n : '0' + n
}

// 3.从自定义模块中导出格式化时间的函数
module.exports = {
  dateFormat
} 
```

02.js文件中：

```javascript
// 导入格式化时间的自定义模块
const TIME = require('./01 格式化时间的传统做法')

// 调用格式化时间的函数
const dt = new Date()
// console.log(dt)
const newDt = TIME.dateFormat(dt)
console.log(newDt)
```

打印结果：

```bash
2022-06-23 06:13:27
```

### 2. 格式化时间的高级做法

1. 使用npm 包管理工具，在项目中安装格式化时间的包 moment

2. 使用 require() 导入格式化时间的包

3. 参考 moment 的官方 API 文档对时间进行格式化

**代码示例**

```javascript
// 1.导入需要的包
// 注意：导入的名称，就是安装包时的名称
const moment = require('moment')

const dt = moment().format('YYYY-MM-DD HH:mm:ss')
console.log(dt)
```

打印结果为：

```bash
2022-06-23 13:21:13
```

### 3. 在项目中安包的命令

如果想在项目中安装指定名称的包，需要运行如下的命令：

```bash
npm install 包的完整名称
```

或简写为：

```bash
npm i 包的名称
```

### 4. 初次安包后多了哪些文件

初次安包完成后，在项目文件夹中多列一个叫做 node_modules 的文件夹 和 package-lock.json 的配置文件。

其中：

- node_modules 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包。

- package-lock.json 配置文件用来记录 node_modules 目录下每一个包的下载信息，如包的名字、版本号、下载地址等。

注意：不要手动修改 node_modules 或 package-lock.json 文件中的任何代码，npm 包管理工具会自动维护他们。

### 5. 安装指定版本的包

默认情况下，使用 npm install 命令安装包时，会自动安装最新版本的包，如果需要安装指定版本的包，可以在包名之后，通过 @ 符号指定具体的版本。

```bash
npm i moment@2.22.2
```

### 6. 包的语义化版本规范

包的版本号是以“点分十进制”形式进行定义的，总共由三位数字，例如2.24.0。

其中每一位数字所代表的含义如下：

- 第一位数字：大版本

- 第二位数字：功能版本

- 第三位数字：Bug修复版本

版本号提升的规则：只要前面的版本号增长了，后面的版本号归零。

## 3.3 包管理配置文件

npm 规定，在项目目录中，必选提供一个叫做 package.json 的包管理配置文件，用来记录与项目有关的一些配置信息，例如：

- 项目的名称、版本号、描述等

- 项目中都用了哪些包

- 哪些包只在开发期间会用到

- 哪些包在开发和部署时都需要用到

### 1. 多人协作问题

遇到的问题：第三方包体积过大，不方便团队成员之间共享项目源代码。

解决方案：共享时删除 node_modules 文件夹

### 2. 如何记录项目中安装了哪些包

在项目根目录中，创建一个叫做 package.json 的配置文件，即可用来记录项目中安装了哪些包。从而方便剔除node_modules，在团队成员之间共享项目的源代码。

注意：把 node_modules 文件夹添加到 .gitignore 忽略文件中。

### 3. 快速创建 package.json

npm 包管理工具提供了一个快捷命令，可以在执行命令所处的目录中，快速创建 package.json 这个包管理配置文件。

```bash
npm init -y
```

注意：

- 上述命令只能在英文目录下成功运行，目录中不能有空格。

- 运行 npm install 命令安装包时，npm 会自动把包的名称和版本号记录到 package.json 中。

### 4. dependencies 节点

在 package.json 文件中，有一个 dependencies 节点，专门用来记录使用 npm install 命令安装了哪些包。

### 5. 一次性安装所有的包

当我们拿到一个剔除了 node_modules 的项目后，需要先把所有的包下载到项目中，才能将项目运行起来。否则会报错。

### 6. 卸载包

可以运行 `npm uninstall` 命令，来卸载指定的包：

```bash
npm uninstall momemt
```

注意：`npm uninstall` 命令执行成功后，会把卸载的包，自动从 package.json 的 dependencies 中移除。

### 7. devDependencies 节点

如果某些包只在项目开发阶段用到，在项目上线之后不会用到，则建议把这些包记录到 devDependencies 节点中。

与之对应，如果某些包在开发和上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

```bash
# 安装指定的包，并记录到 devDependencies 节点
npm i 包名 -D
# 或
npm install 包名 --save-dev
```

## 3.4 解决包下速度慢的问题

### 1. 下载速度慢的原因

npm 下载包时，默认从国外的 https://registry.npmjs.org/ 服务器进行下载，数据传输距离远，因此下包速度慢。

### 2. 使用淘宝npm 镜像服务器

淘宝在国内搭建一个服务器，把国外服务器上的包同步到国内的服务器，然后在国内提供下包的服务。从而极大的提高了下包的速度。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-23-14-48-47-image.png)

扩展：镜像（Mirroring）是一种文件存储形式，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本即为镜像。

### 3. 切换 npm 的下包镜像源

下包的镜像源，指的就是下包的服务器地址。

```bash
# 查看当前的下包镜像源
npm config get registry
# 将下包的镜像源切换为淘宝镜像源
npm confit get registry=http://registry.npmmirror.com
# 检查镜像源是否下载成功
npm config get registry
```

### 4. nrm

为了更方便的切换下包的镜像源，可以安装 nrm 这个小工具，利用nrm 提高的终端命令，可以快速查看和切换下包的镜像源。

```bash
# 通过 npm 全局安装 nrm 工具
npm i nrm -g
# 查看所有可用的镜像源
nrm ls
# 将下包的镜像源切换为 taobao 镜像
nrm use taobao
```

## 3.5 包的分类

### 1. 项目包

安装到项目的 node_modules 中的包，都是项目包。

项目包又分为两类，分别是：

- 开发依赖包（被记录到 devDependencies 节点中的包，只在开发阶段使用）

- 核心依赖包（被记录到 dependencies 节点中的包，在开发和上线之后都会使用）

### 2. 全局包

在执行 npm install 命令时，如果提供了 `-g` 参数，则会把包安装为全局包。

全局包会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下。

```bash
npm i 包名 -g # 全局安装指定的包
npm uninstall 包名 -g # 卸载全局安装的包
```

注意：

- 只有工具性质的包，才有全局安装的必要性，因为它们提供了好用的终端mingl。

- 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明。

## 3.6 规范的包结构

一个规范的包，它的组成结构，必选符号以下 3 点要求：

1. 包必须以单独的目录存在。

2. 包的顶级目录下必须包含 package.json 这个包管理配置文件。

3. package.json 中必须包含 name、version、main 这三个属性，分别代表 包的名字、版本号、包的入口。 

## 3.7 开发属于自己的包

### 1. 包的功能需求

功能需求：

1. 格式化时间

2. HTML的Escape功能（对HTML字符代码进行转义）

3. HTMlL的UnEscape功能（将转义后得字符还原成HTML代码）

### 2. 初识化包的基本结构

1. 新建 tools 文件夹，作为包的根目录

2. 在 tools 文件夹中，新建如下三个文件：
   
   - package.json （包管理配置文件）
   - index.js （包的入口文件）
   - README.md （包的说明文档）

```bash
tools
├─index.js
├─package.json
└─README.md
```

### 3. 初始化 package.json

```json
{
    "name": "tools",
    "version": "1.0.0",
    "main": "index.js", // 指明包的入口
    "description": "提供了格式化时间, HTMLEscape的功能",
    "keywords":["dateFormat","escape"],
    "license": "ISC"
}
```

### 4. 在 index.js 中定义格式化时间的方法

```javascript
// 这是包的入口文件

// 1.定义格式化时间的方法
function dateFormat(dtStr){
  const dt = new Date(dtStr)

  const y = padZero(dt.getFullYear())
  const m = padZero(dt.getMonth() + 1)
  const d = padZero(dt.getDate())

  const hh = padZero(dt.getHours())
  const mm = padZero(dt.getMinutes())
  const ss = padZero(dt.getSeconds())

  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}
// 创建补零函数
function padZero(n){
  return n > 9 ? n : '0' + n
}
// 向外暴露成员
module.exports = {
  dateFormat
} 
```

### 5. 在 index.js 中定义转义 HTML 的方法

```javascript
// 这是包的入口文件

// 1.定义格式化时间的函数
function dateFormat(dtStr){
}
// 创建补零函数
function padZero(n){
}

// 2.定义转义 HTML 字符的函数
function htmlEscape(htmlstr){
  return htmlstr.replace(/<|>|"|&/g, match =>{
    switch(match){
      case '<':
        return '<'
      case '>':
        return '>'
      case '"':
        return '"'
      case '&':
        return '&'
     }
  })
}

// 向外暴露成员
module.exports = {
  dateFormat,
  htmlEscape
}
```

### 6. 在 index.js 中定义还原 HTML 的方法

```javascript
// 这是包的入口文件

// 1.定义格式化时间的函数
function dateFormat(dtStr){
}
// 创建补零函数
function padZero(n){
}

// 2.定义转义 HTML 字符的函数
function htmlEscape(htmlstr){
}

// 3.定义还原 HTML 字符串的函数
function htmlUnEscape(str){
  return htmlstr.replace(/<|>|"|&/g, match =>{
    switch(match){
      case '<':
        return '<'
      case '>':
        return '>'
      case '"':
        return '"'
      case '&':
        return '&'
     }
  })
}

// 向外暴露成员
module.exports = {
  dateFormat,
  htmlEscape,
  htmlUnEscape
}
```

### 7. 将不同的功能进行拆分

1. 将格式化时间的功能，拆分到 tools\src\dateFormat.js 中

2. 将处理 HTML 字符串的功能拆分到 tools\src\htmlEscape.js 中

3. 在 index.js 中，导入两个模块，得到需要的方法

4. 在 index.js 中，把对应的方法共享出去

```bash
tools
│  └─src
│     ├─dateFormat.js
│     └─htmlEscape.js
├─index.js
├─package.json
└─README.md
```

dateFormat.js 文件中：

```javascript
// 1.定义格式化时间的函数
function dateFormat(dtStr){
  const dt = new Date(dtStr)

  const y = padZero(dt.getFullYear())
  const m = padZero(dt.getMonth() + 1)
  const d = padZero(dt.getDate())

  const hh = padZero(dt.getHours())
  const mm = padZero(dt.getMinutes())
  const ss = padZero(dt.getSeconds())

  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}
// 创建补零函数
function padZero(n){
  return n > 9 ? n : '0' + n
}

module.exports = {
  dateFormat
}
```

htmlEscape.js 文件中：

```javascript
// 2.定义转义 HTML 字符的函数
function htmlEscape(htmlstr){
  return htmlstr.replace(/<|>|"|&/g, match =>{
    switch(match){
      case '<':
        return '<'
      case '>':
        return '>'
      case '"':
        return '"'
      case '&':
        return '&'
     }
  }) 
}

// 3.定义还原 HTML 字符串的函数
function htmlUnEscape(str){
  return str.replace(/<|>|"|&/g, match =>{
    switch(match){
      case '<':
        return '<'
      case '>':
        return '>'
      case '"':
        return '"'
      case '&':
        return '&'
     }
  })
}

module.exports = {
  htmlEscape,
  htmlUnEscape
}
```

index.js 文件中：

```javascript
// 这是包的入口文件

const date = require('./src/dateFormat')

const escape = require('./src/htmlEscape')

module.exports = {
  ...date,
  ...escape
}
```

包的使用：

```javascript
const tools = require('./tools/index.js')

// 1.调用 tools.dateFormat() 方法
const dt = tools.dateFormat(new Date())
console.log(dt)

console.log('============')

// 2.调用 tools.htmlEscape() 方法
const htmlStr = `<h1 title="abc">这是h1标签</h1>`
const str = tools.htmlEscape(htmlStr)
console.log(str)

console.log('============')

// 3.调用 tools.htmlUnEscape() 方法
const str2 = tools.htmlUnEscape(str)
console.log(str2)
```

打印结果：

```bash
2022-06-23 17:07:07
============
&lt;h1 title=&quot;abc&quot;&gt;这是h1标签&lt;/h1&gt;
============
<h1 title="abc">这是h1标签</h1>
```

### 8. 编写包的说明文档

README.md 是包的使用说明文档。

README 文件中具体写什么内容，没有强制要求，只要能清晰地把包的作用、用法、注意事项描述清除即可。

## 3.8 发布包

### 1.注册 npm 账号

npm 官网注册即可。

### 2.登录 npm 账号

在终端中执行 `npm login` 命令，依次输入用户名、密码、邮箱后，即可登录成功。

### 3.把包发布的 npm 上

在包的根目录运行 `npm publish` 命令，即可将包发布到 npm上（注意：包名不能雷同）。

### 4.删除已发布的包

运行 `npm unpublish 包名 --force` 命令，即可从 npm 删除已发布的包。

注意：

- npm unpublish 只能删除72小时以内发布的包

- npm unpublish 删除的包，在24小时内不允许重复发布

- 发布包需要谨慎，不要发布没有意义的包

# 4.模块的加载机制

## 4.1 优先从缓存中加载

模块在第一次加载后会被缓存，这也意味着多次调用 require() 不会导致模块的代码被执行多次。

注意：无论是内置模块、自定义模块、第三方模块，都会优先从缓存中加载，从而提高模块的加载效率。

## 4.2 内置模块的加载机制

内置模块由 Node.js 官方提供，内置模块的加载优先级最高。

举例：

```javascript
const fs = require('fs')
```

## 4.3 自定义模块的加载机制

使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。

举例：

```javascript
const tools = require('./tools')
```

同时，在使用 require() 加载自定义模块时，如果省略的文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：

1. 按照确切的文件名进行加载

2. 补全 .js 扩展名进行加载

3. 补全 .json 扩展名进行加载

4. 补全 .node 扩展名进行加载

5. 加载失败，终端报错

## 4.4 第三方模块的加载机制

在加载第三方模块时，Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块。

举例：

```javascript
const moment = require('moment')
```

如果没有找到对应的第三方模块，则移动到上一层父目录中，进行加载，直到文件系统的根目录。

例如，假设在 'D:\node\project\01.js' 文件里调用了 require('moment')，则 Node.js 会按以下顺序查找：

1. <u>D:\node\project</u>\node_modules\moment

2. <u>D:\node</u>\node_modules\moment

3. <u>D:</u>\\node_modules\moment

## 4.5 目录作为模块

当把目录作为模块标识符，传递给 require() 进行加载的时候，由三种加载方式:

1. 在被加载的目录下查找 package.json 文件，并寻找 main 属性，作为 require() 加载的入口。

2. 如果目录中没有 package.json 文件，或者 main 入口不存在，则 Node.js 会试图加载目录下的 index.js 文件。

3. 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'

举例：

```javascript
const tools = require('./tools')
```
