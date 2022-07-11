# 1、XMLHttpREquest的基本使用

## 1.2 使用xhr发起get请求

步骤：

1. 创建 xhr 对象

2. 调用 xhr.open() 函数

3. 调用 xhr.send() 函数

4. 监听 xhr.onreadystatechange 事件

```javascript
// 1.创建 xhr 对象
var xhr = new XMLHttpRequest()
// 2.调用 open 函数，指定 请求方式 和 URL地址
xhr.open('GET','http://www.baidu.com')
// 3.调用 send 函数，发起 Ajax 请求
xhr.send()
// 4.监听 onreadystatechange 事件
xhr.onreadystatechange = function(){
    // 4.1 监听 xhr 的请求状态 readyState，与服务器响应的状态 status
    if(xhr.readyState === 4 && xhr.status === 200){
        // 4.2 打印服务器响应回来的数据
        console.log(xhr.responseText)
    }
}
```

## 1.3 了解xhr对象的readyState属性

readyState属性，用来表示当前Ajax请求所处的状态。

| 值   | 状态               | 描述                                 |
| --- | ---------------- | ---------------------------------- |
| 0   | UNSET            | XMLHttpRequest对象已被创建，但未调用 open 方法。 |
| 1   | OPENED           | open 方法已被调用。                       |
| 2   | HEADERS_RECEIVED | send 方法已被调用，响应头也已经被接收。             |
| 3   | LOADING          | 数据接收中，此时response属性中已经包含部分数据。       |
| 4   | DONE             | Ajax请求完成，数据传输彻底已经完成或失败。            |

## 1.4 使用xhr发起带参数的GET请求

发起带参数的GET请求时，只需在 open 时，为URL地址指定参数即可：

```javascript
xhr.open('GET','http://www.baidu.com?id=1') // ?后面的id=1即为指定的参数
```

这种直接在URL地址后面拼接的参数，叫做查询字符串。

## 1.5 查询字符串

**1.什么是查询字符串**

定义：查询字符串是指在URL的末尾加上用于向服务器发送信息的字符串（变量）。

格式：将英文的?放在URL的末尾，然后加上 参数=值，多个参数直接，使用&进行分割。

```javascript
http://www.baidu.com?id=1&name=jack
```

**2.GET请求携带参数的本质**

无论使用\$.ajax()、\$.get()，还是使用xhr对象发起GET请求，当需要携带参数的时候，本质都是将参数以查询字符串的形式，追加到URL的后面，发送到服务器。

```javascript
$.get('url',{name: 'jack', age: 20},function(){})
// 等价于
$.get('url?name=jack&age=20',function(){})

$.ajax({
    method:'GET',
    url:'url',
    data: {
        name: 'jack',
        age: 18
    },
    success: function(){}
})
// 等价于
$.ajax({
    method:'GET',
    url:'url?name=jack&age=20',
    success: function(){}
})
```

## 1.6 URL编码与解码

**1.什么是URL编码**

URL 地址中，只允许出现英文相关的字母、数字、标点符号，因此，才 URL 地址中不允许出现中文符号。

如果 URL 地址中需要包含中文字符，则必须对中文字符进行编码（转义）。

URL 编码的原则：使用安全的字符（没有特殊用途或特殊意义的可打印字符），去表示那些不安全的字符。

```javascript
http://www.baidu.com?bookname=西游记
// 经过 URL 编码后，URL 地址变为以下格式：
http://www.baidu.com?bookname=%E8%A5%BF%E6%B8%B8%E8%AE%B0
```

每三个表示一个中文字符，%E8%A5%BF：西，%E6%B8%B8：游，E8%AE%B0：记。

**2.如何对URL进行编码与解码**

浏览器提供了URL编码与解码的API，分别是：

- encodeURI() 编码的函数

- decodeURI() 解码的函数

```javascript
encodeURI('黑马')
// 输出字符串 %E9%BB%91%E9%A9%AC
decodeURI('%E9%BB%91%E9%A9%AC')
// 输出字符串 黑马
```

**3.URL编码的注意事项**

由于浏览器会自动对URL地址进行编码操作，因此，大多数情况下，程序员不需要关心URL地址的编码与解码操作。

## 1.7 使用xhr发起POST请求

步骤：

1. 创建xhr对象

2. 调用 xhr.open() 函数

3. 设置 Content-Type 属性（固定写法）

4. 调用 xhr.send() 函数，同时指定要发送的数据

5. 监听 xhr.onreadystatechange 事件

```javascript
var xhr = new XMLHttpRequest()
xhr.open('POST','http://www.baidu.con')
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
xhe.send('bookname=水浒传&author=施耐庵')
xhr.onreadystatechange = function(){
    // 4.1 监听 xhr 的请求状态 readyState，与服务器响应的状态 status
    if(xhr.readyState === 4 && xhr.status === 200){
        // 4.2 打印服务器响应回来的数据
        console.log(xhr.responseText)
    }
}
```

# 2、数据交换格式

## 2.1 什么是数据交换格式

数据交换格式，就是服务器与客户端之间进行数据传输与加号的格式。

前端常用XML和JSON。

## 2.3 JSOM

**1.什么是JSON**

概念：JSON（JavaScript Object Notation）,JavaScript对象表示法。简单来说，JSON就是JavaScript对象和数组的字符串表示法，它使用文本表示一个JS对象或数组的信息。JSON的本质是字符串。

**2.JSON的两种结构**

<mark>对象结构：</mark> 在JSON表示为{}括起来的内容。数据结构为{key: value, key : value}。其中key必须是双引号包裹的字符串，value可以是数字、字符串、布尔值、null、数组、对象 6种类型。

```json
{
    "name": "jack",
    "age": 18,
    "gender": "男"，
    "address": null,
    "hobby": ["吃饭"，"睡觉","打豆豆"]
}
```

<mark>数组结构：</mark> 在JSON表示为[]括起来的内容。数据结构为["jack", 30, true,...]。数组中数据可以是数字、字符串、布尔值、null、数组、对象 6种类型。

```json
["java", "python", "c++"]
[100, 200, 300.5]
[true, false, true]
[{"name": "jack", "age": 18}, {"name": "tom", "age": 20}]
[["苹果", "香蕉"],[1，2]]
```

**3.JSON语法注意事项**

1. 属性名必须使用双引号包裹

2. 字符串类型的值必须使用双引号包裹

3. JSON中不允许使用单引号表示字符串

4. JSON中不能写注释

5. JSON最外层必须是对象或数组格式

6. 不能使用undefined或函数作为JSON的值

**4.JSON和js对象的关系**

```javascript
// 这是一个对象
var obj = {a: 'hello', b: 'world'}
// 这是一个JSON字符串，本质是一个字符串
var json = '{"a": "hello", "b": "world"}'
```

**5.JSON和js对象的互相转换**

从 JSON 字符串到 js对象，又叫做 JSON 反序列化，使用 JSON.parse() 方法：

```javascript
var obj = JSON.parse('{"a": "hello", "b": "world"}')
// 结果是 {a: 'hello', b: 'world'}
```

从 js 对象到 JSON 字符串，又叫做 JSON 序列化，使用 JSON.stringify() 方法：

```javascript
var json = JSON.stringify({a: 'hello', b: 'world'})
// 结果是 '{"a": "hello", "b": "world"}'
```

# 3、封装自己的Ajax函数

## 3.1 要实现的效果

```html
<!-- 1、导入自定义的Ajax函数库 -->
<script src="./jackAjax.js"></scirpt>

<!-- 2、调用自定义的jackAjax函数，发起Ajax请求 -->
<script>
    jackAjax({
        method: '请求类型',
        url: '请求地址',
        data: { /*请求参数对象*/ },
        success: function(res){ // 成功的回调函数
            console.log(res) // 打印数据
        }
    })
</script>
```

## 3.2 定义option参数选项

jackAjax() 函数是我们自定义的 AJax 函数，他接收一个配置对象作为参数，配置对象中可以配置如下属性：

- method ，请求的类型

- url ，请求的URL地址

- data ，请求携带的数据

- success ，请求成功之后的回调函数

## 3.3 处理data参数

需要把 data 对象，转换为查询字符串的格式，从而提交给服务器，因此提前定义 resolveData() 函数如下：

```javascript
function resolveData(data){
    var arr = []
    for (let k in data) {
        arr.push(k + '=' + data[k])
    }
    return arr.join('&')
}
```

## 3.4 定义jackAjax函数

在 jackAjax() 函数中，需要创建 xhr 对象，并监听 onreadystatechange 事件：

```javascript
function jackAjax(options){
    var xhr = new XMLHttpRequest()
    // 把传递过来的参数对象，转换为查询字符串
    var qs = resolveData(options.data)

    // 监听请求状态改变的事件
    xhr.onreadystatechange = function(){
        if(xhr.readyState === 4 && xhr.status === 200){
            var result = JOSN.parse(xhr.responseText)
            options.success(result)
        }
    }
}
```

## 3.5 判断请求的类型

不同的请求类型，对应xhr对象的不同操作，因此需要对请求类型进行判断：

```javascript
function jackAjax(options){
    var xhr = new XMLHttpRequest()
    // 把传递过来的参数对象，转换为查询字符串
    var qs = resolveData(options.data)

    if(options.method.toUpperCase() === 'GET'){
        // 发起GET请求
        xhr.open(options.method, options.url + '?' + qs)
        xhr.send()
    }else if(options.method.toUpperCase() === 'POST'){
        // 发起POST请求
        xhr.open(options.method, options.url)
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        xhr.send(qs)
    }

    // 监听请求状态改变的事件
    xhr.onreadystatechange = function(){
        if(xhr.readyState === 4 && xhr.status === 200){
            var result = JOSN.parse(xhr.responseText)
            options.success(result)
        }
    }
}
```

# 4、XMLHttpRequest Level2的新特性

## 4.1 认识XMLHttpRequest Level2

**1、旧版XMLHttpRequest的缺点**

1. 只支持文本数据的传输，无法用来读取和上传文件

2. 传送和接收数据时，没有进度信息，只能提示有没有完成

**2、XMLHttpRequest Level2的新功能**

1. 可以设置HTTP请求的时限

2. 可以使用FormData对象管理表单数据

3. 可以上传文件

4. 可以获取数据传输的进度信息

## 4.2 设置HTTP请求时限

新版本的 XMLHttpRequest 对象，增加的 timeout 属性，可以设置 HTTP 请求的时限：

```javascript
xhr.timeout = 3000
```

上面的语句，设置最长等待时间为 3000 毫秒，超过了这个时限，就自动停止HTTP请求。与之配套的还有一个timeout时间，用来指定回调函数：

```javascript
xhr.ontimeout = function(evnet){
    alert('请求超时！')
}
```

## 4.3 FormData对象管理表单数据

Ajax 操作往往用来提交表单数据，为了方便表单处理，HTML5 新增了一个 FormData 对象，可以模拟表单操作：

```javascript
// 1、新增 FormData 对象
var fd = new FormData()
// 2、为 FormData 添加表单项
fd.append('uname', 'jack')
fd.append('upwd', '123456')

var xhr = new XMLHttpRequest()
xhr.open('POST', 'http://www.baidu.com')
xhr.send(fd)
xhr.onreadystatechange = function(){}  
```

FormData 对象，也可以用来获取网页表单的值：

```javascript
// 获取表单元素
var form = document.querySelector('#form1')
// 监听表单元素的 submit 事件
form.addEventListener('submit', function(e){
    e.preventDefault()
    // 根据 form 表单创建 FormData 对象，会自动将表单数据填充到 FormData 对象中
    var fd = new FormData(form)
    var xhr = new XMLHttpRequest()
    xhr.open('POST', 'http://www.baidu.com')
    xhr.send(fd)
    xhr.onreadystatechange = function(){}
})
```

## 4.4 上传文件

实现步骤：

1. 定义 UI 结构

2. 验证是否选择了文件

3. 向 FormData 中追加文件

4. 使用 xhr 发起上传文件的请求

5. 监听 onreadystatechange 事件

**1、定义 UI 结构**

```html
<!--1、文件选择框-->
<input type="file" id="file1" />
<!--2、上传按钮-->
<button id="btnUpload">上传文件</button>
<br />
<!--2、显示上传到服务器上的图片-->
<img src="" alt="" id="img" width="800">
```

**2、验证是否选择了文件**

```javascript
// 1、获取上传文件的按钮
var btnUpload = document.querySelector('#btnUpload')
// 2、为按钮添加click事件监听
btnUpload.addEVentListener('click',function(){
    // 3、获取到选择的文件列表
    var files = document.querySelector('file1').files
    if(files.length <= 0){
        return alert('请选择要上传的文件！')
    }
    // 后续业务逻辑
})
```

**3、向 FormData 中追加文件**

```javascript
// 1、创建 FormData 对象
var fd = new FormData()
// 2、向 FormData 中追加文件
fd.append('avater', files[0])
```

**4、使用 xhr 发起上传文件的请求**

```javascript
// 1、创建 xhr 对象
var xhr = new XMLHttpREquest()
// 2、调用 open 函数，指定请求类型和URL地址。其中，请求类型必须为 POST
xhr.open('POST', 'http://www.baidu.com')
// 3、发起请求
xhr.send(fd)
```

**5、监听 onreadystatechange 事件**

```javascript
xhr.onreadystatechange = function(){
    if(xhr.readystate === 4 && xhr.status ===200){
        var data = JSON.parse(xhr.responseText)
        if(data.status === 200){ // 上传成功
             document.querySelector('#img').src = 'http://www.baidu.com' + data.url
        }else{ // 上传失败
            console.log(data.message)
        }

    }
}
```

## 4.5 显示文件上传进度

新版本的 XMLHttpRequest 对象中，可以通过监听 xhr.upload.onprogress 事件，来获取到文件上传的进度。

```javascript
// 创建 xhr 对象
var xhr = new XMLHttpRequest()
// 监听 xhr.upload 的 onprogress 事件
xhr.upload.onprogress = function(e){
    // e.lengthComputable 时一个布尔值，表示当前上传的资源是否具有可计算长度
    if(e.lengthComputable){
        // e.loaded 已传输的字节
        // e.total 需传输的字节
        var percentComplete = Math.ceil((e.loaded/e.total)*100)
    }
} 
```

**1、导入需要的库**



**2、绘制进度条**



**3、监听上传进度的事件**



**4、监听上传完成的事件**



# 5、jQuery高级用法

## 5.1 jQuery实现文件上传

1、定义 UI 结构

```html
<script src="./jquery.js">

<input type="file" id="file1" />
<button id="btnUpload">上传</button>
```

2、验证是否选择了文件

```javascript
$('#btnUpload').on('click',function(){
    var files = $('#file1')[0].files
    if(files.length <= 0){
        return alert('请选择图片后在上传！')
    }
})
```

3、向 FormData 中追加文件

```javascript
// 1、创建 FormData 对象
var fd = new FormData()
// 2、向 FormData 中追加文件
fd.append('avater', files[0])
```

4、使用jQuery发起上传文件的请求

```javascript
$.ajax({
    method: 'POST',
    url: 'http://www.baidu.com',
    data: fd,
    // 不修改 content-Type 属性，使用 FormData 默认的 content-Type 值
    contentType: false,
    //
    processData: false,
    success: function(res){
        console.log(res)
    }
})
```

## 5.2 jQuery实现loading效果

**1、ajaxStart(callback)**

Ajax 请求开始时，执行 ajaxStart 函数。可以在 ajaxStart 的 callback 中显示 loading 效果：

```javascript
$(document).ajaxStart(function(){
    $('#loading').show()    
})
```

注意：$(document).ajaxStart() 会监听当前文档内所有的 Ajax 请求。

**2、ajaxStop(callback)**

Ajax 请求结束时，执行 ajaxStart 函数。可以在 ajaxStart 的 callback 中隐藏 loading 效果：

```javascript
$(document).ajaxStop(function(){
    $('#loading').hide()    
})
```

# 6、axios

## 6.1 什么是axios

Axios 是专注于网络数据请求的库。

相比于原生的 XMLHttpRequset 对象，axios 简单通用。

相比于 jQuery ，axios 更加轻量化，只专注于网络数据请求。

## 6.2 axios发起GET请求

axios 发起 GET 时的语法：

```javascript
axios.get('url', { params: { /*参数*/ } }).then(callback)
```

具体的示例：

```javascript
var url = 'http://www.baidu.com'
var paramsObj = {name: 'jack', age: 20}
axios.get(url, { params: paramsObj }).then(function(res){
    var result = res.data
    console.log(result)
})
```

### 6.3axios发起POST请求

axios 发起 POST 时的语法：

```javascript
axios.post('url', { /*参数*/ } ).then(callback)
```

具体的示例：

```javascript
var url = 'http://www.baidu.com'
var paramsObj = {name: 'jack', age: 20}
axios.post(url, paramsObj).then(function(res){
    var result = res.data
    console.log(result)
})
```

## 6.4 直接使用axios发起请求

1、axios 发起 GET 时的语法：

```javascript
axios({
    method: 'GET',
    url: 'http://www.baidu.com',
    params: { // GET 数据通过 params 属性提供
        name: 'jack',
        age: 18
    }
}).then(function(res){
    console.log(res.data)
})
```

2、axios 发起 POST 时的语法：

```javascript
axios({
    method: 'POSt',
    url: 'http://www.baidu.com',
    data: { // POST 数据通过 data 属性提供
        name: 'jack',
        age: 18
    }
}).then(function(res){
    console.log(res.data)
})
```
