# 1. 基本概念

## 1.1 URL的概念

URL（全称是UniformResourceLocator）中文叫统一资源定位符，用于标识互联网上每个资源的唯一存放位置。

浏览器只有通过URL地址，才能正确的定位资源的存放位置，从而访问对应的资源。

## 1.2  URL地址的组成部分

URL地址一般由三部分组成：

1. 客户端与服务器之间的通信协议

2. 存放该资源的服务器名称

3. 资源在服务器上具体的存放位置

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-27-13-55-05-image.png)

## 1.3 网页的打开过程

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-27-11-35-15-image.png)

- 客户端与服务器之间的通信过程，分为 **请求-处理-响应** 三个步骤。

- 网页中的任何一个资源，都是通过 **请求-处理-响应** 的方式从服务器获取回来的。

## 1.4 基于浏览器的开发者工具分析通信过程

1. 打开 Chrome 浏览器

2. `ctrl + shift + i` 打开 Chrome 的开发者工具

3. 切换到 Network 面板

4. 选中 Doc 标签

5. 刷新页面，分析客户端与服务器端的通信过程

## 1.5 XMLHttpRequest对象

网页资源有文本、图片、视频、音频、数据等。

只要是资源，必要通过 请求-处理-响应 的方式进行获取。

如果在网页中请求服务器中的数据资源，则需要用到 XMLHttpRequest 对象。

XMLHttpRequest（简称 xhr）是浏览器提供的 js 成员。通过它，可以请求服务器上的数据资源。

```javascript
// xhr最简单的用法
var xhrObj = new XMLHttpRequest()
```

## 1.6 资源请求的方式（get和post）

最常见的两种请求方式分别是 get 和 post 请求。

- get请求，通常用于向服务器取回资源。

- post请求，通常用于向服务器发送资源。

# 2. 了解Ajax

Ajax 的全称是 Asynchronous Javascript and XML（异步 JavaScript 和 XML）。

通常认为，在网页中利用 xhr 对象和服务器进行数据交互的方式，就是Ajax。

# 3. jQuery中的Ajax

浏览器中提供的 XMLHttpRequest 用法比较辅助，jQuery 对 XMLHttpRequest 进行了封装，提供了一系列Ajax函数，极大地降低了 Ajax 地使用难度。

jQuery 中发起 Ajax 请求最常用地三个方法：

- $.get()

- $.post()

- $.ajax()

### 3.1 $.get() 函数

$.get() 的语法格式：

```javascript
$.get(url,[data],[callback])
```

其中，三个参数的含义为：

| 参数名      | 参数类型     | 是否必选 | 说明           |
|:--------:|:--------:|:----:|:------------:|
| url      | string   | 是    | 要请求的资源地址     |
| data     | object   | 否    | 请求资源期间要携带的参数 |
| callback | function | 否    | 请求成功时的回调函数   |

**1、发起不带参数的请求**

```javascript
$.get('https://www.baidu.com', function(res){
    console.log(res) // res 是服务器返回的数据对象
}
```

**2、发起带参数的请求**

```javascript
$.get('https://www.baidu.com', {id: 1}, function(res){
    console.log(res)
}
```

## 3.2 $.post() 函数

$.post() 的语法格式：

```javascript
$.post(url,[data],[callback])
```

其中，三个参数的含义为：

| 参数名      | 参数类型     | 是否必选 | 说明         |
|:--------:|:--------:|:----:|:----------:|
| url      | string   | 是    | 提交数据的地址    |
| data     | object   | 否    | 要提交的数据     |
| callback | function | 否    | 提交成功时的回调函数 |

**提交数据的示例代码**

```javascript
$.post(
    'https://www.baidu.com', 
    {id: 1, name: 'jack'},
    function(res){
        console.log(res)
}
```

## 3.3 $.ajax() 函数

$.ajax() 的语法格式：

```javascript
$.ajax({
    type: '', // 请求的方式，GET 或 POST
    url: '', // 请求的 url 地址
    data: '', // 这次请求要携带的数据
    success:function(res){} // 请求成功后的回调函数
})
```

使用 $.ajax() 发起 get 请求

```javascript
$.ajax({
    type: 'GET',
    url: 'https://www.baidu.com',
    data:{
        id: 1
    },
    success:function(res){
        console.log(res)
    }
})
```

使用 $.ajax() 发起 post 请求

```javascript
$.ajax({
    type: 'POST',
    url: 'https://www.baidu.com',
    data:{
        name: 'jack',
        address: '中国河北'
    },
    success:function(res){
        console.log(res)
    }
})
```

# 4. 接口

使用 Ajax 请求数据时，被请求的 url 地址，就叫做数据接口（简称接口）。同时，每个接口必须有请求方式。

接口测试工具：postman。

### 4.1 接口文档

接口文档，顾名思义就是接口的说明文档，告诉我们怎么发送和接收数据。应包含以下6项内容：

1. 接口名称：用来标识各个接口的简单说明，例如登录接口、获取图书列表接口等。

2. 接口 URL：接口的调用地址。

3. 调用方式：GET 和 POST。

4. 参数格式：接口需要传递的参数，每个参数必须包含参数名称、参数类型、是否必选、参数说明这4项内容。

5. 响应格式：接口的返回值的详细描述，一般包括数据名称、数据类型、说明3项內容。

6. 返回示例（可选）：通过对象的形式，举例服务器返回数据的结构。

# 5. 案例

## 案例01-图书管理

获取图书列表（核心代码）

```javascript
function getBookList(){
    // 1.发起 Ajax 请求获取图书列表数据
    $.get('https://www.baidu.com',function(){
        // 2.获取数据是否成功（status===200为获取成功）
        if(res.status !== 200) return alert(''获取数据失败！)
        // 3.渲染页面结构
        var rows = []
        // 4.循环拼接字符串
        $.each(res.data,function(i,item){
            rows.push('<tr><td>' + item.id + '</td><td>' + item.bookname + '</td></tr>' )
        })
        // 5.渲染表格结构
        $(‘#bookBody’).empty().append(rows.join(''))
    }
}
```

删除图书（核心代码）

添加图书（核心代码）

## 案例02-聊天机器人
