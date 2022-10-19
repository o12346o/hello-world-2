# 1. 初识 Node.js

## 1.1 回顾与思考

**1. 已经掌握哪些技术**

HTML、CSS、JavaScript

**2. 浏览器中的 JavaScript 的组成部分**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-22-16-02-11-image.png)

**3. 思考：为什么 JavaScript 可以在浏览器中被执行**

<img title="" src="file:///C:/Users/maxuanbo/AppData/Roaming/marktext/images/2022-06-22-16-03-48-image.png" alt="" width="525">

**4. 思考：为什么 JavaScript 可以操作 DOM 和 BOM**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-22-16-05-02-image.png)

**5. 浏览器中的 JavaScript 运行环境**

运行环境是指代码正常运行所需的必要环境。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-22-16-07-32-image.png)

**6. 思考 JavaScript 能否做后端开发**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-22-16-09-17-image.png)

## 1.2 Node.js 简介

### 1. 什么是Node.js

Node.js  是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

### 2. Node.js 中的 JavaScript 运行环境

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-22-15-47-23-image.png)

注意：

1. 浏览器是 JavaScript 的前端运行环境。

2. Node.js 是 JavaScript 的后端运行环境。

3. Node.js 中无法调用 DOM 和 BOM 等浏览器内置API。

### 3. Node.js 可以做什么

1. 基于 Express 框架（ http://www.expressjs.com.cn/ ），可以快速构建 Web 应用

2. 基于 Electron 框架（ https://electronjs.org/ ），可以构建跨平台的桌面应用

3. 基于 restify 框架（ http://restify.com/ ），可以构建 API 接口项目

4. 读写和操作数据库，创建实用的命令行工具辅助前端开发，等等...

### 4. Node.js 怎么学

浏览器中的 JavaScript 的学习路径：

JavaScript 基础语法 + 浏览器内置 API（DOM + BOM） + 第三方库（jQuery、art-template 等）

Node.js 的学习路径：

JavaScript 基础语法 + Node.js 内置 API 模块（fs、path、http 等） + 第三方 API 模块（ express、mysql 等 ）

## 1.3 Node.js 环境的安装

如果希望通过 Node.js 来运行 JavaScript 代码，则必须安装 Node.js 环境才行。

进入 Node.js 的官网（ https://nodejs.org/en/ ）,选择 LTS 版本安装包，安装包下载完成，安装提示安装即可。![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-22-16-18-20-image.png)

**1. 区分 LTS 版本和 Current 版本的不同**

1. LTS 为长期稳定版

2. Current 为新特性常新版

**2. 查看已安装的 Node.js 的版本号**

打开终端，在终端输入命令 `node -v` 后，按下回车键，即可查看已安装的 Node.js 的版本号。

## 1.4 使用Node运行js代码

### 1. node打开js

1. 打开cmd；
2. 输入 `node`  + `要执行的js文件的路径`。 

或

1. 打开 要执行的js文件的目录；
2. <kbd>shift</kbd>+<kbd>右键</kbd> ，打开powershell；
3. 运行 `node` + ` 要执行的js文件的路径`。

### 2. 终端中的快捷键

1. 使用 <kbd>上箭头</kbd> ，快速定位到上一次命令；
2. 使用 <kbd>tab</kbd> ，自动补充js文件名/文件路径；
3. 使用 <kbd>esc</kbd> ，快速清空当前已输入的命令；
4. 输入 `cls` ，清空终端。

# 2. fs 文件系统模块

## 2.1 什么是 fs 文件系统模块

- fs.readFile()，读取指定文件中的内容

- fs.writeFlie()，向指定文件写入

**导入 fs 模块**

```javascript
const fs = require('fs')
```

## 2.2 读取指定文件中的内容

### 1. fs.readFile() 的语法格式

```javascript
fs.readFile(path[, options], callback)
```

- 参数1：必选参数，字符串，表示文件路径。
- 参数2：可选参数，表示以什么编码格式来读取文件。
- 参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

### 2. fs.readFile() 示例代码

以 utf8 编码为示例

```javascript
// 1. 导入 fs 模块
const fs = require('fs')

// 2. 调用 fs.readFile() 方法来读取文件
fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
  console.log(err)
  console.log('------')
  console.log(dataStr)
})
```

### 3. 判断文件是否读取成功

读取成功时 ，err的值为null。

```javascript
// 1. 导入 fs 模块
const fs = require('fs')

// 2. 调用 fs.readFile() 方法来读取文件
fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
  if(err){
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
})
```

## 2.3 向指定的文件中写入内容

### 1. fs.writeFile() 的语法格式

向指定的文件路径中，写入文件内容：

```javascript
fs.writeFile(path, data[, options], callback)
```

- 参数1：必选参数，字符串，表示文件路径。
- 参数2：必选参数，表示要写入的内容。
- 参数3：可选参数，表示以什么编码格式来读取文件，默认为 utf8 。
- 参数4：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

### 2. fs.writeFile() 示例代码

```js
// 1.导入 fs 文件系统模块
const fs = require('fs')

// 2.调用fs.writeFile()方法，写入文件内容
fs.writeFile('./files/2.txt','hello node!',function(err){
    // 2.1如果文件写入成功，则 err 的值等于 null
    // 2.2如果文件写入失败，则 err 的值等于一个 错误对象
    console.log(err)
}
```

### 3. 判断文件是否写入成功

可以判断 err 对象 是否为 null ，从而知晓文件写入的结果：

```js
// 1.导入 fs 文件系统模块
const fs = require('fs')

// 2.调用fs.writeFile()方法，写入文件内容
fs.writeFile('./files/2.txt','hello node!',function(err){
   if(err){
        return console.log('文件写入失败！', + err.message)
    }
    console.log('文件写入成功！')
}
```

## 2.5 练习 - 考试成绩整理

使用 fs 文件系统模块，将 files目录下 <u>成绩.tx</u>t 文件中的考试数据，整理到 <u>成绩-ok.txt</u>  文件中。

整理前，<u>成绩.txt</u> 文件中的数据格式如下：

```
小红=99 小白=100 小黄=70 小黑=66 小绿=88
```

整理完成后，希望得到的 <u>成绩-ok.txt</u> 文件中的数据格式如下：

```
小红,99
小白,100
小黄,70
小黑,66
小绿,88
```

**实现核心步骤**

1. 导入需要的 fs 文件系统模块

2. 使用 fs.readFile() 方法，读取 <u>成绩.txt</u> 文件

3. 判断文件是否读取失败

4. 文件读取成功后，处理成绩数据

5. 将处理完成的成绩数据，调用 fs.writeFile() 方法，写入到新文件 <u>成绩-ok.txt</u> 文件中

**实现代码**

```javascript
// 1.导入 fs 模块
const fs = require(''fs)


// 2.调用 fs.readFile() 方法，读取文件的内容
fs.readFile('./files/成绩.txt', 'utf8', function(err,dataStr){
    // 3.判断是否读取成功
    if(err){
        return console.log('读取文件失败！'  err.meaage+)
    }

    // 4.读取文件成功
    // 4.1 先把成绩的数据，按照空格进行分割
    const arrOld = dataStr.split(' ')
    // 4.2 循环分割后的数组，对每一项数据，进行字符串的替换操作
    const arrNew = []
    arrOld.forEach(item => {
        arrNew.push(item.replace('=', ':'))
    })
    // 4.3 把新数据的每一项，进行合并，得到一个新的字符串
    const newStr = arrNew.join('\r\n')

    // 5.调用 fs.writeFile() 方法，把处理完成的成绩，写入到新文件中
    fs.writeFile('./files/成绩-ok.txt', newStr, function(err){
        if(err){
            return console.log('写入文件失败！' + err.message)
        }
        console.log('成绩写入成功')    
    }
}
```

## 2.6 fs 模块 - 路径动态拼接的问题

在使用 fs 模块时，如果使用的是以`./` 或 `../`开头的相对路径，很容易出现路径拼接错误的问题。

<mark>原因</mark>：代码执行时，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。

> **文件结构**
> 
> 注释：`插入制表符的方法：使用输入法中的几何符号。`
> 
> ```
> D:
> └─ day
>     └─ test
>         ├─ files
>         │    └─ 1.txt 
>         └─ a.js
> ```
> 
> **在 D:day文件夹中运行 node 命令**
> 
> ```bash
> node .\test\a.js
> ```
> 
> **a.js文件中：**
> 
> ```javascript
> const fs = require('fs')
> 
> fs.readFile('./files/1.txt', 'utf8', > function(err,dateStr){
>     if(err){
>     return console.log('读取文件失败！' + err.message)
>     }
>     console.log('读取文件成功！')
> }
> ```
> 
> **调用 fs.readFile() 方法 拼接的路径为：D:day\\files\\1.txt，路径错误**

<mark>解决方法：</mark>

方法一：直接提供完整路径，移植性差，不利于维护。

```javascript
const fs = require('fs')

// 提供完整路径，移植性差，不利于维护
fs.readFile('D:day\\test\\files\\1.txt', 'utf8', > function(err,dateStr){
    if(err){
    return console.log('读取文件失败！' + err.message)
    }
    console.log('读取文件成功！')
}
```

方法二：__dirname 表示当前文件所处的目录。

```javascript
const fs = require('fs')

// __dirname 表示当前文件所处的路径
fs.readFile(__dirname + '/files/1.txt', 'utf8', > function(err,dateStr){
    if(err){
    return console.log('读取文件失败！' + err.message)
    }
    console.log('读取文件成功！')
}
```

# 3. path 路径模块

## 3.1 什么是 path 模块

path 模块是 Node.js 官方提供的、预览处理路径的模块，他提供了一系列的方法和属性，用来满足用户对路径的处理需求。

- path.join() 方法 ，连接多个路径。
- path.basename() 方法 ，从路径字符串中，解析出文件名。
- path.extname() 方法，从路径字符串中方，获取文件的扩展名。

**导入模块**

```javascript
const path = require('path')
```

## 3.2 路径拼接

### 1. path.join() 的语法格式

```javascript
path.join([...paths])
```

### 2. path.join() 的代码示例

```javascript
// 1. 导入 path 代码块
const path = require('path')

// 使用 path.join() 方法
const pathStr = path.join('/a','/b/c','../','./d')
console.log(pathStr) // 输出 \a\b\d\e

const pathStr2 = path.join(__dirname,'./files/1.txt')
console.log(pathStr2) // 输出 当前文件所在目录\files\1.txt
```

注意：拼接路径时，推荐使用path.join()方法，不要直接使用 加号 拼接路径

## 3.3 获取路径中的文件名

### 1. path.basename() 的语法格式

```javascript
path.basename(path[,ext])
```

参数解读：

- path：必选参数，表示一个路径的字符串

- ext：可选参数，表示文件扩展名

### 2.path.basename() 的语法格式

```javascript
// 1. 导入 path 模块
const path = require('path')

// 2. 使用 path.basename() 方法
const fpath = '/a/b/a/index.html' // 定义文件的存放路径

// 2.1 不排除文件扩展名
const fullName = path.basename(fpath)
console.log(fullName) // 输出 index.html
// 2.2 排除文件扩展名
const nameWithoutExt = path.basename(fpath,'html')
console.log(nameWithoutExt) // 输出 index
```

## 3.4 获取路径中的文件扩展名

### 1. path.extname() 的语法格式

```javascript
path.extname(path)
```

参数解读：

- path：必选参数，表示一个路径的字符串

返回值：

- 返回值为 得到的 扩展名 字符串

### 2. path.extname() 的代码示例

```javascript
// 1. 导入 path 模块
const path = require('path') 

// 2. 使用 path.extname() 方法，获取扩展名
const fpath = '/a/b/c/index.html'  // 定义文件路径字符串

const fext = path.extname(fpath)
console.log(fext) // 输出 .html
```

# 4. http 模块

## 4.1 什么是 http 模块

http 模块 是 Node.js 官方提供的、用来创建 web 服务器 的模块。

通过 http 模块 提供的 `http.createServer()` 方法，就能方便的把一台普通的电脑，变为一台 Web 服务器，从而对外提供 Web资源服务。

**导入模块**

```javascript
const http = require('http')
```

## 4.2 进一步理解 http 模块的作用

服务器和普通电脑的区别在于，服务器上安装了 web 服务器软件，例如：IIS、Apache等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。

在 Node.js 中，不需要IIS、Apache等这些第三方 web 服务器软件。可以基于 Node.js 提供的 http 模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务。

## 4.3 服务器相关的概念

**1. ip 地址**

ip 地址是互联网上每台计算机的唯一地址，ip 地址具有有唯一性。

IP 地址的格式：用“点分十进制”表示成a.b.c.d 的形式，其中每一项都在0~255直接。例如，168.192.1.1（路由器管理地址）。

- 互联网中每台 web 服务器都有自己的 IP 地址。例如，可以 `ping www.baidu.com` ,可以查看到百度服务器的 IP 地址。

- 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入 127.0.0.1 这个 IP 地址，就能把自己的电脑当做一台服务器进行访问了。

**2. 域名和域名服务器**

IP 地址 和 域名（Domain name） 是一一对应的关系，这份对应关系存放在叫做域名服务器（DNS，Domain name server）的电脑中。

域名服务器提供 IP 地址和域名之间的转换服务。通过域名即可访问对应 IP 地址的服务器。

- 单纯使用 IP 地址，互联网中的电脑也能够正常工作，但是有了域名的加持，互联更加方便。

- 在开发测试期间，127.0.0.1 对应的域名是 localhost，都代表了本机，使用效果没有任何区别。

**3. 端口号**

在一台计算机中，可以运行成百上千个 web 服务，每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 web 服务进行处理。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-23-09-05-00-image.png)

- 每个端口号不能同时被多个 web 服务占用。

- 在实际应用中，URL 中的 80 端口可以被省略（其他端口号不能）。 

- 【举例】localhost:80 和 localhost 都是访问 80 端口。

## 4.4 创建最基本的 web 服务器

### 1.创建 web 服务器的基本步骤

1. 导入 http 模块

2. 创建 web 服务器实例

3. 为服务器绑定 request 事件，监听客户端的请求

4. 启动服务器

### 2. 创建 web 服务器的代码示例

```javascript
// 1. 导入 http 模块
const http = require('http')
// 2. 创建 Web 服务器实例
const server = http.createServer()
// 3. 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request',function(req,res){
    console.log('Someone visit our web server.')
})
// 4. 启动服务器
server.listen(8080,function(){
    console.log('server running at http://127.0.0.1:8080')
})
```

### 3. req 请求对象

只要服务器收到了客户端的请求，就会调用通过 server.on() 为服务器绑定的 request 事件处理函数。

如果想在事件处理函数中，访问与客户端相关的数据或属性，可以使用以下方式：

```javascript
server.on('request',(req) => {
    // req 是请求对象，它包含了与客户段相关的数据和属性，例如：
    // req.url 是客户段请求的 URL 地址
    // req.method 是客户端的 method 请求类型
    const str = `Your request url is ${req.url}, and request method is ${req.method}`  
    console.log(str)
})
```

### 4. res 响应对象

在服务器的request 事件处理函数中，如果想要访问与服务器相关的数据或属性，可以使用以下方式：

```javascript
server.on('request',(req,res) => {
    // res 是响应对象，它包含了与服务器相关的数据和属性，例如：
    // 要发送到客户端的字符串
    const str = `Your request url is ${req,url}, and request method is ${req.method}`  
    // res.end() 方法的作用：
    // 向客户端发送指定的内容，并结束这次请求的处理过程
    res.end(str)
})
```

### 5. 解决中文乱码问题

当调用 res.end() 方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式：

```javascript
server.on('request',(req,res) => {
    // 发送的内容包含中文
    const str = `您请求的 url 地址是 ${req.url}，请求的 method 类型是 ${req.method}`
    // 为了防止中文显示乱码的问题，需要设置响应头 Content-Type 的值为 text/html:charset=utf-8
    res.setHeader('Content-Type','text/html:charset=utf-8')
    // 把包含中文的内容，响应给客户端
    res.end(str)
})
```

## 4.4 根据不同的 url 响应不同的 html 内容

### 1. 核心实现步骤

1. 获取请求的 url 地址

2. 设置默认的响应内容为 404 Not found

3. 判断用户请求的 url 地址

4. 设置 Content-Type 响应头，防止中文乱码

5. 使用 res.send() 把内容响应给客户端

### 2. 动态响应内容

```javascript
server.on('request',(req,res) => {
    // 1.获取请求的 url 地址
    const url = req.url
    // 2.设置默认的响应内容为 404 Not found
    let content = `<h1>404 Not found</h1>`
    // 3.判断用户请求的 url 地址
    if(url === ‘/’ || url === '/index.html'){
        content = `<h1>首页</h1>`
    }else if(url === '/about.html'){
        content = `<h1>关于页面</h1>`
    }
    // 4.设置 Content-Type 响应头，防止中文乱码
    res.setHeader('Content-Type','text/html:charset=utf-8')
    // 5.把内容响应给客户端
    res.end(content)
})
```
