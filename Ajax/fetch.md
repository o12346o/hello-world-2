# 1. fetch API

`Fetch API`提供了一个 JavaScript 接口，用于访问和操纵HTTP的请求和响应等。提供了一个全局 `fetch()`方法来跨网络异步获取资源。

# 2. 与AJAX的区别

Fetch 规范与 jQuery.ajax() 主要有三种方式的不同：

- 当接收到一个代表错误的 HTTP 状态码， 即使响应的 HTTP 状态码是 404 或 500。从 `fetch()` 返回的 Promise **不会被标记为 reject，**相反，会标记为 resolve （但是会把 resolve 的返回值的 `ok` 属性设置为 false ），**仅当网络故障时或请求被阻止时，才会标记为 reject**。
- `fetch()` 可以接收跨域 cookies；也可以使用 `fetch()` 建立起跨域会话。
- `fetch` 不会发送 cookies。

# 3. Fetch() 使用

给`fetch()` 提供一个参数指明资源路径，会返回一个包含响应结果的promise。当然它只是一个 HTTP 响应，为了获取JSON的内容，我们需要使用 [`json()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Body/json) 方法：

默认发送GET请求：

```js
fetch('http://example.com/movies.json')    
  .then(response => response.json())
  .then(data => console.log(data))
```

带参数的GET请求：

```js
var id=1
fetch(`https://www.easy-mock.com/mock/5f507e38a758c95f67d6eb42/fetch/getmsg?id=${id}`)    
.then(response => response.json())
.then(data => console.log(data))
```

发送POST请求

```js
var data={
    id:'1',
}
fetch('https://www.easy-mock.com/mock/5f507e38a758c95f67d6eb42/fetch/postmsg',{
    method:'POST',
    body:data
})    
.then(response => response.json())
.then(data => console.log(data))
```
