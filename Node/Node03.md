# 1. 初识 Express

## 1.1 Express简介

**1、什么是Express**

Express 和 Node 内置的 http 模块类似，是专门用来创建 Web 服务器的。

**2、Express能做什么**

对于前端程序员，最常见的两种服务器。分别是：

- Web 网站服务器，专门对外提供 Web 网页资源的服务器。

- API 接口服务器，专门对外提供 API 接口的服务器。

使用 Express，可以方便、快速的创建 Web 网站服务器或 API 接口服务器。

## 1.2 Express的基本使用

**1、安装**

```javascript
npm i express@4.17.1
```

**2、创建基本的 Web 服务器**

```javascript
// 1、导入 express
const express = require('express')
// 2、创建 Web 服务器
const app = express()
// 3、调用 app.listen(端口号，启动成功后的回调函数)，启动服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1')
})
```

**3、监听 GET 请求**

通过 app.get() 方法，可以监听客户端的 GET 请求

```javascript
// 参数1：客户端请求的 URL 地址
// 参数2：请求对应的处理函数
//    req：请求对象（包含了与请求相关的属性与方法）
//    res：响应对象（包含了与响应相关的属性与方法）
app.get('请求url', function(req, res){ /* 处理函数 */ })
```

**4、监听 POST 请求**

通过 app.POST() 方法，可以监听客户端的 POST 请求

```javascript
// 参数1：客户端请求的 URL 地址
// 参数2：请求对应的处理函数
//    req：请求对象（包含了与请求相关的属性与方法）
//    res：响应对象（包含了与响应相关的属性与方法）
app.post('请求url', function(req, res){ /* 处理函数 */ })
```

**5、把内容响应给客户端**

通过 app.send() 方法，可以把处理好的内容，发送给客户端

```javascript
app.get('请求url', (req, res) => {
    //向客户端发送 JSON 对象
    res.send({name: 'jaxk', age: 20})
})

app.post('请求url', (req, res) => {
    //向客户端发送文本内容
    res.send('请求成功')
})
```

**6、获取 URL 中携带的查询参数**

通过 req.query 对象，可以访问到客户端通过查询字符串的，发送到服务器的参数

```javascript
app.get('/', (req, res) => {
  // req.query 默认是一个空对象
  // 客户端使用 ?name=jack&age=20 这种查询字符串的形式，发送到服务器的参数,
  // 可以通过 req.query 对象访问到，例如：
  // req.query.name    req.query.age
  console.log(req.query)
})
```

**7、获取 URL 中的动态参数**

通过 req.params 对象，可以访问 URL 中，通过 : 匹配到的动态参数

```javascript
app.get('/user:id', (req, res) => {
  // req.params 默认是一个空对象
  // 里面存放着通过 : 动态匹配的参数值
  console.log(req.params)
})
```

## 1.3 托管静态资源

**1、express.static()**  

express 提供了一个非常好用的函数，叫做 express.static()，通过它，可以非常方便的创建一个静态资源服务器。

例如，通过以下代码，就可以将 public 目录下的图片、CSS文件、Javascript文件对外开发访问了：

```javascript
app.use(express.static('public'))
```

现在，你就可以访问 public 目录中的所有文件了：

http://localhost:80/images/01.png

http://localhost:80/css/index.css

注意：Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在 URL 中。

**2、托管多个静态资源目录**

如果要托管多个静态资源目录，请多次调用 express.static() 函数

```javascript
app.use(express.static('public'))
app.use(express.static('files'))
```

访问静态资源文件时，express.static() 会根据目录的添加顺序查找所需的文件。

**3、挂载路径前缀**

如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用以下方式：

```javascript
app.use('/public',express.static('public'))
```

现在，你就可以访问 public 目录中的所有文件了：

http://localhost:80/public/images/01.png

http://localhost:80/public/css/index.css

## 1.4 nodemon

**1、为什么要使用 nodemon**

在编写调试 Node.js 项目的适合，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。

可以使用 nodemon （ https://www.npmjs.com/package/nodemon ）这个工具，它能够监听项目文件的变动，当代码被修改后，nodemon 会字段帮我们重启项目，极大方便了开发和测试。

**2、安装 nodemon**

```javascript
npm install -g nodemon
```

**3、使用 nodemon**

当基于 Node.js 编写了一个网站应用的时候，传统的方式，使用 node app.js 命令，来启动项目。

现在，可以将 node 命令替换为 nodemon 命令，使用 nodemon app.js 命令，来启动项目。代码被修改后，会被 nodemon 监听到，从而实现自动重启项目的效果。

```javascript
node app.js
// 替换为：
nodemon app.js
```

# 2. Ecxpress 路由

## 2.1 路由的概念

**1、什么是路由**

广义上来讲，路由就是映射关系。

**2、Express 中的路由**

在 Express 中，路由是指客户端的请求与服务器处理函数之间的映射关系。

Express 路由由 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数，格式如下：

```javascript
app.METHOD(PATH, HANDLER)
```

**3、Express 中的路由的例子**

```javascript
// 请求类型为 GET，请求的 URL 为 /
app.get('/', function(req, res){
    res.send('GET请求!')
})

// 请求类型为 POST，请求的 URL 为 /
app.post('/', function(req, res){
    res.send('POST请求!')
})
```

**4、路由的匹配过程**

每当一个请求到达服务器后，需要先经过路由的匹配，只有匹配成功后，才会调用对应的处理函数。

在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的URL同时匹配成功，则 Express 会将这次请求，转交给对应的处理函数进行处理。

## 2.2 路由的使用

**1、最简单的用法**

在 Express 中使用路由最简单的方式，就是把路由挂载到 app 上，示例如下：

```javascript
const express = require('express')
const app = express()

app.get('/', (req,res) => {res.send('get')})
app.post('/', (req,res) => {res.send('post')})

app.listen(80, () => {console.log(server running at http://127.0.0.1)})
```

**2、模块化路由**

为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。

将路由抽离为单独模块的步骤如下：

1. 创建路由模块对应的 js 文件

2. 调用 express.Router() 函数创建路由对象

3. 向路由对象上挂载具体的luy

4. 使用 moudule.exports 向外共享路由对象

5. 使用 app.use() 函数注册路由模块

**3、创建路由模块**

```javascript
// 这是路由模块

// 1、导入 express
const express = require('express')
// 2、创建路由对象
const router = express.Router()


// 3、挂载具体的路由
router.get('/user', (req, res) => {
  res.send('get')
})
router.post('/user', (req, res) => {
  res.send('post')
})


// 4、向外导出路由对象
module.exports = router
```

**4、注册路由模块**

```javascript
const express = require('express')
const app = express()


// 1、导入路由模块
const userRouter = require('./04 router')

// 2、使用 app.use() 注册路由模块
app.use(userRouter)

//注意：app.use() 函数的作用，就是用来注册全局中间件

app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```

**5、为路由模块添加前缀**

类似于托管静态资源，路由模块添加前缀的方式也很简单，就是在注册时添加前缀即可：

```javascript
app.use('/api', userRouter)
```

# 3. Express 中间件

## 3.1 中间件的概念

**1、什么是中间件**

中间件（Middleware），特指业务流程的中间处理环节。

**2、Express 中间件的调用流程**

当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-19-15-43-16-image.png)

**3、Express 中间件的格式**

Express 中间件，本质是一个 function 处理函数，Express 中间件的格式如下：

```javascript
app.get('/', function(req, res, next){
    next()
})
```

注意：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。

**4、next 函数的作用**

next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-19-15-49-15-image.png)

## 3.2 中间件的使用

**1、定义中间件函数**

```javascript
const mw = function(req, res, next){
  console.log('这是一个最简单的中间件函数')
  // 注意：在当前中间件的业务处理完毕后，必须调用 next() 函数
  // 表示把流转关系转交给下一个中间件或路由
  next()
}
```

**2、全局生效的中间件**

客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。

通过 app.use(中间件函数)，即可定义一个全局生效的中间件，示例代码如下：

```javascript
// 注册全局生效的中间件
app.use(mw)
```

**3、定义全局中间件的简化形式**

```javascript
// 定义全局中间件的简化形式
app.use(function(req, res, next) {
    console.log('定义全局中间件的简化形式')
    next()
})
```

**4、中间件的作用**

多个中间件直接，共享同一份 req 和 res 。基于这样的特性，可以在上游的中间件中，统一为 req 或 res 对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

```javascript
// 定义全局中间件的简化形式
app.use((req, res, next) => {
   //Date() 得到是时间戳，new Date() 得到的是时间对象。 
    const time = Date.now()
    // const date = new Date()
    req.startTime = time
    next()
})

app.get('/', (req, res) => {
  res.send('Home Pgae ' + req.startTime)
})
app.get('/user', (req, res) => {
  res.send('User Pgae ' + req.startTime)
})
```

**5、定义多个全局组件**

可以使用 app.use() 连续定义多个全局中间件，客户端请求到达服务器之后，会按照中间件的注册顺序依次进行调用。

**6、局部生效的中间件**

不使用 app.use() 定义的中间件，叫做局部生效的中间件，示例代码如下：

```javascript
// 定义局部中间件
const mw1 = function(req, res, next) {
  console.log('局部中间件')
  next()
}
// mw1 这个中间件只在当前路由中生效
app.get('/', mw1, (req, res) => {
  res.send('Home Pgae ')
})
// mw1 这个中间件不会影响下面这个路由
app.get('/user', (req, res) => {
  res.send('User Pgae ')
})
```

**7、定义多个局部中间件**

可以在路由中，使用多个局部中间件

```javascript
// 方式一
app.get('/', mw1, mw2, (req, res) => {res.send('home page')})
// 方式二
app.get('/',[mw1, mw2], (req, res) => {res.send('home page')})
```

**8、中间件的5个使用注意事项**

1. 一定要在路由之前注册中间件

2. 客户端发送过来的请求，可以连续调用多个中间件进行处理

3. 执行完中间件的业务代码后，一定不要忘记 next()

4. 为了防止代码逻辑错误，next() 后不要再写代码

5. 连续调用多个中间件时，多个中间之间，共享 req 和 res 对象

## 3.3 中间件的分类

Express 官方把常见的中间件，分成了5大类：

1. 应用级别的中间件

2. 路由级别的中间件

3. 错误级别的中间件

4. Express 内置的中间件

5. 第三方的中间件

**1、应用级别的中间件**

通过 app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件，叫做应用级别的中间件。

```javascript
app.use((req, res, next)=> {
    next()
})
app.get('/', mw1, (req, res) => {
    res.send('home page')
})
```

**2、路由级别的中间件**

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级中间件没有任何区别，只不过，应用级别的中间件绑定到 app 实例上，路由级别的中间件绑定到 router 实例上。

```javascript
const express = require('express')
const app = express()
const router = express.Router()

// 路由级别的中间件
router.use(function(req, res, next) {
    console.log('time',Date.now())
    next()
})
app.use('/', router)
```

**3、错误级别的中间件**

错误级别的中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

格式：错误级别的中间件的 function 处理函数中，必须有4个参数，形参顺序从前到后，分别是(err, req, res, next)。

```javascript
app.get('/',(req, res) => {                    // 1、路由
    throw new Error('服务器内部发生了错误！')     // 1.1 描述一个自定义的错误
    res.send('home page')
})
app.use(function(err, req, res, next){        // 2、错误级别的中间件
    console.log('发生了错误' + err.message)    // 2.1 在服务器端打印错误消息
    res.send('Error!' + err.message)         // 2.2 在客户端响应错误信息
})
```

**4、Express内置的中间件**

自 Expresss 4.16.0 版本开始，Express内置了3个常用中间件：

1. express.static() 快速托管静态资源的中间件。

2. express.json() 解析 JSON 格式的请求体数据。

3. express.urlencoded() 解析 URL-encoded 格式的请求体数据。

```javascript
// 通过 express.json() 这个中间件，解析表单中 JSON 格式的数据
app.use(express.json())
// 通过 express.urlencoded() 这个中间件，来解析表单中的 url-encoded 格式的数据
app.use(express.urlencoded({ extended: false}))
```

**5、第三方的中间件**

以 body-parser 为例子，第三方的中间件使用步骤：

1. 运行`npm i body-aprser`命令，安装中间件 

2. 使用 require() 导入中间件

3. 调用 app.use() 注册并使用中间件

```javascript
const parser = require('body-parser')
app.use(parser.urlencoded({ extend: false}))
```

## 3.4 自定义中间件

**1、需求描述与实现步骤**

自动手动模拟依赖类似于 express.urlencoded 这样的中间件，来解析 POST 提交到服务器的表单数据。

实现步骤：

1. 定义中间件

2. 监听 req 的 data 事件

3. 监听 req 的 end 事件

4. 使用 querystring 模块解析请求体数据

5. 将解析出来的数据对象挂载为 req.body

6. 将自定义中间件封装为模块

**2、定义中间件**

使用 app.use() 来定义全局生效的中间件。

```javascript
app.use(function(req, res, next){
    next()
})
```

**3、监听 req 的 data 事件**

在中间件中，需要监听 req 对象的 data 事件，来获取客户端发送到服务器的数据。

如果数据量较大，无法一次发送完毕，则客户端会把数据切割后，分批发送到服务器，所以 data 事件可能会触发多次，每一次触发 data 事件，获取到的数据只是完整数据的一部分，需要手动对接收到的数据进行拼接。

```javascript
let str = ''
// 监听req对象的data事件（客户端发送过来的新的请求体数据）
req.on('data', (chunk) => {
    // 拼接请求体数据
    str += chunk
}) 
```

**4、监听 req 的 end 事件**

当请求体数据接收完毕后，会自动触发 req 的 end 事件。

因此，可以在 req 的 end 事件中，拿到并处理完整的请求体数据。

```javascript
req.on('end', () => {
    console.log(str)
})
```

**5、使用 querystring 模块解析请求体数据**

Node 内置了一个 querystring 模块，专门用来处理查询字符串。通过这个模块提供的 parse() 函数，可以轻松的把查询字符串，解析成对象的格式。

```javascript
// 导入 node 内置 querystring
const qs = require('querystring')

// 调用 qs.parse()，把查询字符串解析为对象
const body = qs.parse(str)
```

**6、将解析出来的数据对象挂载为 req.body**

上游的中间件合下游的中间件及路由之间，共享同一份 req 和 res 。因此，可以将解析出来的数据，挂载为 req 的自定义属性，命名为 req.body，供下游使用。

```javascript
req.on('end', () => {
    const body = qs.parse(str)
    req.body = body
    next()
})
```

**7、将自定义中间件封装为模块**

为了优化代码结构，把自定义的中间件函数，封装为独立的模块。

```javascript
// custom-body-parser.js 模块
const qs = require('querystring')
function bodyParser(req, res, next){ /* 业务代码 */}
module.exports = bodyParser // 向外导出解析请求体数据的中间件函数
```

```javascript
// 1、导入自定义的中间件模块
const myBodyParser = require('custom-body-parser')
// 2、注册自定义的中间件模块
app.use(myBodyParser)
```

# 4. 使用 Express 写接口

## 4.1 创建基本的服务器

app.js 文件中

```javascript
// 1、导入 express
const express = require('express')
// 2、创建 Web 服务器
const app = express()

/* 业务代码... */

// 3、调用 app.listen(端口号，启动成功后的回调函数)，启动服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1')
})
```

## 4.2 创建 API 路由模块

apiRouter.js 文件中

```javascript
// 【路由模块】
const express = require('express')
const router = express.Router()

// 3、挂载具体的路由
/* 业务代码... */

// 4、向外导出路由对象
module.exports = router
```

app.js 文件中

```javascript
//【导入并注册路由模块】
const userRouter = require('./16 apiRouter')
app.use('/api', userRouter)
```

## 4.3 编写 GET 接口

```javascript
// 【路由模块】
router.get('/get', (req, res) => {
    // 1、获取客户端通过查询字符串，发送到服务器的数据
    const query = req.query
    // 2、把数据响应给客户端
    res.send({
        status: 0,              // 状态，0表示成功，1表示失败
        msg: 'GET请求成功！',    // 状态描述
        data: query            // 需要响应个客户端的具体数据
    })
})
```

## 4.4 编写 POST 接口

```javascript
// 【路由模块】
router.post('/post', (req, res) => {
    // 1、获取客户端通过请求体，发送到服务器的 URL-encoded 数据
    const body = req.body
    // 2、把数据响应给客户端
    res.send({
        status: 0,              // 状态，0表示成功，1表示失败
        msg: 'POST请求成功！',    // 状态描述
        data: query            // 需要响应个客户端的具体数据
    })
})
```

注意：如果要获取 URL-encoded 格式的请求体数据，必须配置中间件 app.use(express.urlencoded({ extended: false }))

## 4.5 cors 跨域资源共享

**1、接口的跨域问题**

上面编写的 GET 和 POST 接口，不支持跨域请求。

解决接口跨域问题的方案主要有两种：

1. CORS（主流的解决方案，推荐使用）

2. JOSNP（有缺陷的解决方案，只支持 GET 请求）

**2、使用 cors 中间件解决跨域问题**

cors 是 Express 的一个第三方中间件，通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

使用步骤：

1. 运行 `npm install cors` 安装中间件

2. 使用 `const cors = require('cors')` 导入中间件

3. 在路由之前调用 `app.use(cors())` 配置中间件

**3、什么是 cors**

CORS（Cross-Origin Resource Sharing，跨域资源共享）有一系列 HTTP 响应头组成，这些 HTTP 响应同决定浏览器是否阻止前端 JS 代码跨域获取资源。

浏览器的同源安全策略默认会阻止网页跨域获取资源。但是，如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以接口浏览器的跨域访问限制。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-20-12-57-10-image.png)

**4、CORS 的注意事项**

CORS 主要在服务器端进行配置，客户端浏览器无锡做任何额外的配置，即可请求开启了CORS 的接口。

CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level 2 的浏览器，菜鸟正常访问开启了 CORS 的服务器端接口（例如：IE10+、Chrome4+、FireFox3.5+）。 

**5、CORS 响应头部  Access-Control-Allow-Origin**

响应头部可以携带一个 Access-Control-Allow-Origin 字段，其语法如下：

```
Access-Control_Allow-Origin: <origin> | *
```

其中，origin 参数的值指定了允许访问资源的外域 URL。

例如，下面的字段值将只允许来自 http://127.0.0.1 的请求：

```javascript
res.setHeader('Access-Control_Allow-Origin', 'http://127.0.0.1')
```

如果指定了Access-Control-Allow-Origin 字段的值为通配符\*，表示允许来自任何域的请求：ja

```javascript
res.setHeader('Access-Control_Allow-Origin', '*')
```

**6、CORS 响应头部 Access-Control-Allow-Headers**

默认情况下，CORS 只支持客户端向服务器发送如下的 9 个请求头：

1. Accept

2. Accept-Language

3. Content-Language

4. DPR

5. DownLink

6. Save-Data

7. Viewport-Width

8. Width

9. Content-Type（值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

示例代码：

```javascript
// 允许客户端额外向服务器端发送 Content-Type 请求头 和 x-Custom-Header 请求头
// 注意：多个请求头之间用英文逗号进行分隔
res.setHeader('Access-Control_Allow-Headers', 'Content-Type, x-Custom-Header')
```

**7、CORS 响应头部 Access-Control-Allow-Methods**

默认情况下，CORS 只支持客户端发起 GET、POST、HEAD 请求。

如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Allow-Methods 来指明事项请求所允许使用的 HTTP 方法。

示例代码：

```javascript
// 只允许 POST、GET、DELETE、HEAD 请求方法
res.setHeader('Access-Control-Allow-Methods', 'POST, GET, DELETE, HEAD')
// 允许所有的 HTTP 请求方法
res.setHeader('Access-Control-Allow-Methods', '*')
```

**8、CORS 请求的分类**

客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：

1. 简单请求

2. 预检请求

**9、简单请求**

同时满足以下两大条件的请求，就属于简单请求：

1. 请求方式：GET、POST、HEAD 三者之一。

2. HTTP 头部信息不超过以下几种字段：
   
   - Accept
   
   - Accept-Language
   
   - Content-Language
   
   - DPR
   
   - DownLink
   
   - Save-Data
   
   - Viewport-Width
   
   - Width
   
   - Content-Type（值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

**10、预检请求**

只要符号以下任何一个条件的请求，都需要进行预检请求：

1. 请求方式：GET、POST、HEAD 之外的请求类型。

2. 请求头中包含自定义头部字段。

3. 向服务器发送了 application/json 格式的数据。

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求之后，才会发送真正的请求，并且携带真实数据。

**11、简单请求和预检请求的区别**

简单请求的特点：客户端与服务器之间只会发送一次请求。

预检请求的特点：客户端与服务器之间会发送两次请求，OPTION 预检请求成功之后，才会发起真正的请求。

## 4.6 编写JSOPNP接口

**1、JSONP的概念**

浏览器通过 script 标签的 src 属性，球球服务器上的数据，同时，服务器返回一个函数的调用，这种请求数据的方式叫做 JSONP。

**2、创建 JSONP 接口的注意事项**

如果项目中已经配置了 CORS 跨域资源共享，为了防止冲突，必须在配置 CORS 中间件之前声明 JSONP 的接口。否则，JSONP 接口会被处理成开启了 CORS 的接口。

```javascript
// 先创建 jsonp 接口
app.get('/api/jsonp', (req, res) => {})

// 再配置 cors 中间件（后续所有的接口，都会被处理成 cors 接口）
app,.use(cors())

// 这是一个开启了 CORS 的接口
app.get('/api/get', (req, res) => {})
```

**3、实现 JSONP 接口的步骤**

1. 获取客户端发送过来的回调函数的名字

2. 得到要通过 JSONP 形式发送给客户端的数据

3. 根据前两步得到的数据，拼接出一个函数调用的字符串

4. 把上一步拼接好的字符串，响应给客户端的 script 标签进行解析执行

**4、实现 JSONP 接口的具体代码**

```javascript
// 1、 获取客户端发送过来的回调函数的名字
const funcName = req.query.callback
// 2、 得到要通过 JSONP 形式发送给客户端的数据
const data = {name: 'jack', age: 18}
// 3、 根据前两步得到的数据，拼接出一个函数调用的字符串
const scriptStr = `${funcName}(${JSON.stringify(data)})`
// 4、 把上一步拼接好的字符串，响应给客户端的 script 标签进行解析执行
res.send(scriptStr)
```

**5、在网页中使用 jQuery 发起 JSONP 请求** 

调用 \$.ajax() 函数，提供 JSONP 的配置选项，从而发起 JSONP 请求。

```javascript
$('#btnJSONP').on('click', function () {
      $.ajax({
        type: 'GET',
        url: 'http://127.0.0.1/api/jsonp',
        dataType: 'jsonp',
        success: function (res) {
          console.log(res)
        }
      })
    })
```