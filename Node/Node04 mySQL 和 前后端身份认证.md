# 1. 数据库的基本原理

**1、常见数据库及分类**

- 关系型数据库（SQL数据库）：
  
  - MySQL 数据库
  
  - Oracle 数据库
  
  - SQL Server 数据库

- 非关系型数据库（NoSQL数据库）：
  
  - Mongodb 数据库

**2、实际开发中 库、表、行、字段 的关系**

- 在实际项目开发中，一般情况下，每个项目对应独立的数据库。

- 不同的数据，存储到数据库中不同的表中。

- 每个表中存储哪些信息，由字段决定。

- 表中的每一行，代表每一条具体的数据。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-11-25-14-image.png)

# 2. 安装并配置 MySQL

**1、安装方式**

1. msi 安装文件（需要安装）

2. zip 压缩包（解压后直接使用）

**2、zip 压缩包方式**

1. 环境变量配置
   
   - 我的电脑->属性->高级->环境变量，选择Path,在其后面添加: 你的mysql bin文件夹的路径 。

2. 进入安装目录的bin文件夹
   
   - 以<mark>管理员身份</mark>运行cmd命令：mysqld --initialize-insecure --user=mysql。
   - 等待完成后，会在安装目录生成data文件夹，打开文件夹，找到 .err 文件。发形随机产生的临时密码为空密码。
   - 执行`mysqld install`  安装 mysql。
     - 当出现安装失败时，可能是由于以前安装过mysql，未卸载完全。执行  `sc query mysql`查看是否有mysql，执行`sc delete mysql`清除以前的安装数据。然后重新安装即可。

3. 启动 MySql 服务
   
   - 启动，net start mysql
   
   - 停止，net stop mysql

4. MySql 登录
   
   - 登录，mysql -u root -p
     
     - 服务启动成功之后，需要登录的时候输入命令输入密码
     - 第一次登录没有密码，直接按回车
   
   - 修改密码
     
     - net start mysql 
     - mysqladmin -u root -p password
     - 输入新密码
   
   - MySQL版本8.0.4之后修改密码
     
     - 登录 mysql
     
     - ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';

**3、Navicat图形化界面连接mysql**

文件 -> 新建连接 -> 连接 ip 和 密码，自定义连接名 -> 完成连接。

# 3. MySQL 的基本使用

## 3.1 创建数据库

```sql
create database my_db_01;
```

## 3.2 创建数据表

新建表，设置字段。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-12-42-59-image.png)

以下为SQL语法：

```sql
CREATE TABLE `my_users` (
  `id` int unsigned NOT NULL AUTO_INCREMENT COMMENT '用户唯一id',
  `username` varchar(255) NOT NULL COMMENT '用户名',
  `password` varchar(255) NOT NULL COMMENT '用户密码',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

## 3.3 在数据表中写入数据

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-12-59-48-image.png)

以下为SQL语法：

```sql
insert into my_users (username,password) values('jack','123456');
-- 或 insert into `my_users` (`username`,`password`) values('jack','123456');
```

## 3.4 使用 SQL 管理据库

**1、什么是SQL**

SQL（Structured Query Language）是结构化查询语言，专门用来访问和处理数据库的编程语言。

- SQL 是一门数据库编程语言

- 使用 SQL 语言编写出来的代码，叫做 SQL 语句

- SQL 只能在关系型数据库中使用。非关系型数据库不支持SQL 语言。

**2、SQL 语句**

# 4. 在项目中操作 MySQL

## 4.1 在项目中操作数据库的步骤

1. 安装操作 MySQL 数据库的第三方模块（mysql）

2. 通过 mysql 模块连接到 MySQL 数据库

3. 通过mysql 模块执行 SQL 语句

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-13-15-27-image.png)

## 4.2 安装与配置 mysql 模块

**1、安装 mysql 模块**

mysql 模块是 npm 的第三方模块，它提供了在 Node 项目中连接和操作 MySQL数据库的能力。

```powershell
npm install mysql
```

**2、配置 mysql 模块**

在使用 mysql 模块操作 MySQL 数据库之前，必须先对 mysql 模块进行必要的配置。

```javascript
// 1、导入数据库
const mysql = require('mysql')
// 2、建立与 MySQL 数据库的连接关系
const db = mysql.createPool({
  host: '127.0.0.1', // 数据库的 IP 地址
  user: 'root', // 登录数据库的账号
  password: '', // 登录数据库的密码
  database: 'my_db_01' // 指定要操作哪个数据库
})
```

**3、测试 mysql 模块能否正常工作**

调用 db.query() 函数，指定要执行的 SQL 语句，通过回调函数拿到执行的结果。

```javascript
// 测试 mysql 模块能否正常工作
db.query('select 1', (err, results) => {
  // mysql 模块种子期间报错了
  if(err) return console.log('ERR!!!!',err.message)
  // 能够成功的执行 SQL 语句
  console.log(results)
})
```

## 4.3 使用 mysql 模块操作 MySQL 数据库

**1、查询数据**

```javascript
// 查询 my_users 表中的所有数据
const sqlStr = 'select * from users'
db.query(sqlStr, (err, results) => {
  // SQL执行失败
  if(err) return console.log(err.message)
  // SQL执行成功
  console.log(results)
})
```

**2、插入数据**

```javascript
// 插入数据
// 1、要插入到 users 表中的数据对象
const user = {username: 'Man', password: 'pcc321'}
// 2、待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'INSERT INTO users (username, password) VALUES (?, ?)'
// 3、使用数组的形式，依次为 ? 占位符指定具体的值
db.query(sqlStr, [user.username, user.password], (err, results) => {
  // SQL执行失败
  if(err) return console.log(err.message)
  // SQL执行成功
  console.log(results)
  if(results.affectedRows ===1 ) console.log('插入数据成功！')
})
```

**3、插入数据的便捷方式**

如果数据对象的每个属性和数据表的字段一一对应，则可以通过以下方式快速插入数据：

```javascript
// 插入数据的便捷方式
// 1、要插入到 users 表中的数据对象
const user = {username: 'grace', password: 'qqqqq'}
// 2、待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'INSERT INTO users SET ?'
// 3、直接将数据对象当作占位符的值
db.query(sqlStr, user, (err, results) => {
  // SQL执行失败
  if(err) return console.log(err.message)
  // SQL执行成功
  console.log(results)
  if(results.affectedRows ===1 ) console.log('插入数据成功！')
})
```

**4、更新数据**

```javascript
// 更新数据
// 1、要更新到 users 表中的数据对象
const user = { id: 10, username: 'bob', password: 'qqqqq'}
// 2、待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'UPDATE users SET username=?, password=? WHERE id=?'
// 3、直接将数据对象当作占位符的值
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
  // SQL执行失败
  if(err) return console.log(err.message)
  // SQL执行成功
  console.log(results)
  if(results.affectedRows ===1 ) console.log('更新数据成功！')
})
```

**5、更新数据的便捷方式**

```javascript
// 更新数据
// 1、要更新到 users 表中的数据对象
const user = { id: 10, username: 'bob', password: 'qqqqq'}
// 2、待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'UPDATE users SET ? WHERE id=?'
// 3、直接将数据对象当作占位符的值
db.query(sqlStr, [user, user.id], (err, results) => {
  // SQL执行失败
  if(err) return console.log(err.message)
  // SQL执行成功
  console.log(results)
  if(results.affectedRows ===1 ) console.log('更新数据成功！')
})
```

**6、删除数据**

```javascript
// 删除数据
// 1、待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'DELETE FROM users WHERE id=?'
// 2、为占位符指定具体的值
db.query(sqlStr, 10, (err, results) => {
  // SQL执行失败
  if(err) return console.log(err.message)
  // SQL执行成功
  console.log(results)
  if(results.affectedRows ===1 ) console.log('删除数据成功！')
})
```

**7、标记删除**

使用 DELETE 语句，会把真正的数据从表中删除，为了保险起见，推荐使用标记删除的形式，来模拟删除的动作。

所谓标记删除，就是在表中设置类似于 status 这样的字段，来标记当前这条数据是否被删除。

当用户执行了删除的动作时，并没有执行 DELETE 语句把数据删除掉，而是执行了 UPDATE 语句，将这条数据对应的 status 字段标记为删除即可。

```javascript
// 标记删除：使用 UPDATE 代替 DELETE 语句，只更新数据的状态，并没有真正的删除
// 1、待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'UPDATE users SET status=1 WHERE id=?'
// 2、为占位符指定具体的值
db.query(sqlStr, 5, (err, results) => {
  // 2.1 SQL执行错误
  if(err) return console.log(err.message)
  // 2.2 SQL执行完毕
  console.log(results)
  // 2.2.1 标记删除失败
  if(results.affectedRows ===0 ) console.log('标记删除失败')
  // 2.2.2 标记删除成功
  if(results.affectedRows ===1 ) console.log('标记删除成功！')
})
```

# 5. 前后端的身份认证

## 5.1 Web 开发模式

目前主流的 Web 开发模式有两种:

1. 基于 服务端渲染 的传统 Web 开发模式

2. 基于 前后端分离 的新型 Web 开发模式

**1、基于 服务端渲染 的传统 Web 开发模式**

服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不需要 Ajax 这样的技术额外请求页面的数据。

```javascript
app.get('/index.html', (req, res) => {
    const user = {name: 'jack', age: 20}
    const html = `<h1>姓名：${user.name}, 年龄：${user.age}</h1>`
    res.send(html)
})
```

**2、服务器渲染的优缺点**

优点：

- 前端耗时少，浏览器只需要直接渲染页面即可。

- 有利于 SEO，因为服务器响应的是完整的 HTML 页面内容，所以爬虫更容易获取信息，更利于 SEO。

缺点：

- 占用服务器端资源。即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。

- 不利于前后端分离，开发效率低。使用服务器渲染，则无法进行分工合作。

**3、基于 前后端分离 的新型 Web 开发模式**

前后端分离：依赖于 Ajax 技术的广泛应用，后端只负责 API 接口，前端使用 Ajax 调用接口。

**4、前后端分离的优缺点**

优点：

- 开发体验好。前端专注于 UI 页面的开发，后端专注于 api 的开发。

- 用户体验好。可以轻松实现页面的局部刷新。

- 减轻了服务器的渲染压力。页面最终在每个用户的浏览器中生成。

缺点：

- 不利于 SEO。爬虫无法爬取页面的有效信息。解决方案：利用 Vue、React 等前端框架的 SSR（svever side render）技术恩公很好的解决 SEO 问题。

## 5.2 身份认证

**1、什么是身份认证**

身份认证（Authentication），通过一定的手段，完成对用户身份的确认。

例如，指纹解锁、支付密码、手机验证码登录、邮箱密码登录、二维码登陆等。

**2、不同开发模式下的身份认证**

- 服务器渲染 推荐使用 Session 认证机制

- 前后端分离 推荐使用 JWT 认证机制

## 5.3 Session 认证机制

**1、HTTP 协议的无状态性**

HTTP 协议的无状态性，是指客户端的每次 HTTP 请求都是独立的，连续多个请求之间没有之间的关系，服务器不会主动保留每次 HTTP 请求的状态。

例如，

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-16-21-35-image.png)

**2、如何突破 HTTP 无状态的限制**

对于超市而言，超市通过会员卡来辨别用户的会员身份。

<img src="file:///C:/Users/maxuanbo/AppData/Roaming/marktext/images/2022-07-21-16-22-40-image.png" title="" alt="" width="649">

注意：现实生活中的会员身份认证方式，在 Web 开发中叫做 Cookie。

**3、什么是 Cookie**

Cookie 是存储在用户浏览器中的一段不超过 4KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的可选属性组成。

不同域名下的 Cookie 是各自独立的，每当客户端发起请求，会自动把当前域名下的所有未过期的 Cookie 一同发送到服务器。

Cookie 的几大特性：

1. 自动发送

2. 域名独立

3. 过期时限

4. 4KB 限制

**4、Cookie 在身份认证中的作用**

客户端第一次请求服务器时，服务器通过响应头的形式，向客户端发送一个身份认证的 Cookie ，客户端会自动将 Cookie 保存在浏览器中。

随后，当客户端浏览器每次请求服务器的时候，浏览器会自动将身份认证相关的 Cookie，通过请求头的形式发送个服务器，服务器即可验明客户端的身份。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-16-33-50-image.png)

**5、Cookie 不具有安全性**

由于 Cookie 是存储在浏览器中的，而且浏览器页提供了访问 Cookie API，因此 Cookie 很容易被伪造，不具有安全性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送被浏览器。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-16-39-47-image.png)

**6、提高身份认证的安全性**

为了防止客户伪造会员卡，需要进行会员卡认证。只有认证通过的会员卡，才能被正常使用。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-16-42-17-image.png)

这种 “会员卡” + “刷卡认证” 的设计理念，就是 Session 认证机制的精髓。

**7、Session 的工作原理**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-16-44-04-image.png)

## 5.4 在 Express 中使用 Session 认证

**1、安装 express-session 中间件**

在 Express 项目中，只需安装 epxress-session 中间件，接口在项目中使用 Session 认证。

```powershell
npm install express-sesssion
```

**2、配置 express-session 中间件**

```javascript
const session = require('express-session')
application.use(
  session({
    secret: 'jack',           // secret 属性的值可以为任意的字符串
    resave: false,            // 固定写法
    saveUninitialized: true   // 固定写法
  })
)
```

**3、向 session 中村数据**

当 express-session 中间件配置成功后，即可通过 req.session 来访问和使用 session 对象，从而存储用户的关键信息。

```javascript
app.post('/api/login', (req, res) => {
  if(req.body.username !== 'admin' || req.body.password !== '000000'){
    return res.send({status: 1, msg: '登录失败'})
  }

  req.session.user = req.body // 将用户的信息，存储到 Session 中
  req.session.isLogin = ture  // 将用户的登录状态，存储到 Session 中
})
```

**4、从 session 中取数据**

可以直接哦从 req.session 对象上获取之前存储的数据。

```javascript
// 从 Session 中取数据，获取用户姓名
app.get('/api/username', (req, res) => {
  // 判断用户是否登录
  if(!req.session.isLogin){
    return res.send({status: 1, msg: 'fail'})
  }
  res.send({
    status: 0,
    msg: 'success',
    username: req.session.user.username
  })
})
```

**5、清空 session**

调用 req.session.destroy() 函数，即可清空服务器保存的当前用户的 session 信息。

```javascript
// 清空 session 的数据
app.post('/api/logout', (req, res) => {
  req.session.destroy()
  res.send({
    status: 0,
    msg: '退出登录成功！',
  })
})
```

**6、session的过期时间**

session 和 cookie 一样，默认在浏览关闭后失效。重新打开浏览器后原来的 session 已经不存在。

可以设置 session 和cookie 的过期时间，使得在浏览器重启后，仍能使用原来的 session 和 cookie 。

## 5.5 JWT 认证机制

**1、Session 认证的局限性**

Session 认证机制需要配合 cookie 才能实现。由于 cookie 默认不支持跨域访问，所以当涉及到前端跨域请求后端接口的时候，需要做很多额外的工作，才能实现跨域 session 认证。

注意：

- 当前端请求后端接口不存在跨域问题的时候，推荐使用 Session 身份认证机制。

- 当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证机制。

**2、什么是 JWT**

JWT（JSON Web Token）是目前最流行的跨域认证解决方案。

**3、JWT 的工作原理**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-21-20-39-59-image.png)

用户的信息通过 Token 字符串的形式，保存在客户端浏览器中，服务器通过还原 Token 字符串的形式来认证用户的身份。

**4、JWT 的组成部分**

JWT 通常由三部分组成，分别是 Header（头部）、Payload（有效载荷）、Signature（签名）。

三者之间用英文的句号分隔，格式如下：

```
Header.Payload.Signature
```

**5、JWT 的三个部分各自代表的含义**

- Payload 部分才是真正的用户信息，它是用户信息经过加密后生成的字符串。

- Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-22-09-30-28-image.png)

**6、JWT 的使用方式**

客户端收到服务器返回的 JWT 后，会将它存储在 localStorage 或 sessionStorage 中。

此后，客户端每次与服务器通信，都要带上这个 JWT 字符串，从而进行身份认证。推荐的做法是把 JWT 放在 HTTP 请求头的 Authorization 字段中，格式如下：

```
Authorization: Bearer <token>
```

## 5.6 在 Express 中使用 JWT

**1、安装 JWT 相关的包**

```powershell
npm install jsonwebtoken express-jwt
```

其中：

- jsonwebtoken 用于生成 JWT 字符串

- express-jwt 用于将 JWT 字符串解析还原成 JSON 对象

**2、导入 JWT 相关的包**

```javascript
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')
```

**3、定义 secret 密钥**

为了保证 JWT 字符串的安全性，防止 JWT 字符串在网络传输过程中被别人破解，需要专门定义一个用于加密和解密的 secret 密钥：

- 当生成 JWT 字符串的时候，需要使用 secret 密钥对用户的信息进行加密，最终得到加密好的 JWT 字符串。

- 当把 JWT 字符串解析还原成 JSON 对象的时候，需要使用 secret 密钥进行解密。

```javascript
// secret 密钥的本质就是一个字符串
const secretKey = 'jack'
```

**4、在登录成功后生成 JWT 字符串**

调用 jsonwebtoken 提供的 sign() 方法，将用户的信息加密成 JWT 字符串，响应给客户端：

```javascript
// 登录接口
app.post('/api/login', function(req, res) {
  // 登录失败的代码...
  // 登录成功
  // TODO 03:在登录成功之后，调用 jwt.sign() 方法生成 JEWT 字符串，并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的密钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  const tokenStr = jwt.sign({username: userinfo.username}, secretKey, {expiresIn: '30s'})
  res.send({
    status: 200,
    msg: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})
```

**5、将 JWT 字符串还原为 JSON 对象**

客户端每次在访问那些有权限接口的时候，都需要主动通过请求头中的 Authorization 字段，将 Token 字符串发送到服务器进行身份认证。

此时，服务器可以通过 express-jwt 这个中间件，自动将客户端发送过来的 Token 解析还原成 JSON 对象。

```javascript
// TODO 04:注册将 JWT 字符串解析还原成 JHON 对象的中间件
// expressJWt({secret: secretKey}) 就是用来解析 Token 的中间件
// .unless({path: [/^\/api\//] }) 用来指定哪些接口不需要访问权限
app.use(expressJWt({secret: secretKey})).unless({path: [/^\/api\//] })
```

**6、使用 req.auth 获取用户信息**

当 express-jwt 这个中间件配置成功之后，即可在哪些有权限的接口中，使用 req.auth 对象，来访问 JWT 字符串中解析出来的用户信息了。

```javascript
// 这是一个有权限的接口
app.get('/admin/getinfo', function(req, res) {
  // TODO 05:使用 req.user 获取用户信息，并使用 data 属性将用户的信息发送给客户端
  console.log(req.auth)
  res.send({
    status: 200,
    msg: '获取用户信息成功！',
    data: req.auth // 要发送给客户端的用户信息
  })
})
```

**7、捕获解析 JWT 失败后产生的错误**

当使用 express-jwt 解析 Token 字符串时，如果客户端发送过来的 Token 字符串过期或不合法，会产生一个解析失败的错误，影响项目的正常运行。我们可以通过 Express 的错误中间件，捕获这个错误并进行相关的处理。

```javascript
// TODO 06:使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 这次错误是由 token 解析失败导致的
  if(err.name === 'UnauthorizedError'){
    return res.send({
      status: 401,
      msg: '无效的token'
    })
  }
  // 其他原因导致的错误
  res.send({
    status: 500,
    msg: '未知的错误'
  })
})
```
