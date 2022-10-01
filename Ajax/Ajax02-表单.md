# 1.表单

## 1.1 什么是表单

表单在网页中主要负责数据采集功能。HTML中的 form 标签，就是用于采集用户输入的信息，并通过 form 标签的提交操作，把采集到的信息提交到服务器端进行处理。

## 1.2 表单的组成部分

表单由三个基本部分组成：

- 表单标签

- 表单域

- 表单按钮

```html
<form>
    <input type="text" name="username">
    <input type="password" name="password">
    <button type="submit">提交</button>
</form>
```

## 1.3 form 标签的属性

form 标签用来采集数据，form 标签的属性则是用来规定如何包采集到的数据发送到服务器。

| 属性      | 值                                                                          | 描述                         |
| ------- | -------------------------------------------------------------------------- | -------------------------- |
| action  | url地址                                                                      | 规定当提交表单时，向何处发送表单数据。        |
| method  | get或post                                                                   | 规定以何种方式把表单提交到 action url中。 |
| enctype | application/x-www-form-urlencoded <br/>multipart/form-data <br/>text/plain | 规定在发送表单数据之前如何对其进行编码。       |
| target  | _blank<br/>_self<br/>_parent <br/>_top <br/>framename                      | 规定在何处打开 action url。        |

### 1.3.1 action

action属性用来指明跳转的url地址。

未规定时，默认为当前的url地址。
提交表单后，会立即跳转。

### 1.3.2 method

method属性用来指明提交方法。

get适合用于提交少量、简单的数据。
post适合用于提交大量的、复杂的、或包含文件上传的数据。

### 1.3.3 enctype

enctype属性用来指明在发送数据之前如何对数据进行编码。

| 值                                 | 描述                      |
| --------------------------------- | ----------------------- |
| application/x-www-form-urlencoded | 在发送前编码所有字符。(默认)         |
| multipart/form-data               | 不对字符编码。                 |
| text/plain                        | 空格转换为加号，但不对特殊字符编码。（很少用） |

在上传文件时，必须为multipart/form-data。

如果不涉及文件上传操作，则之间将enctype的值设置为 application/x-www-form-urlencoded 即可。

### 1.3.4 target

target属性用来指明在何处打开 action url。

| 值         | 描述        |
| --------- | --------- |
| _blank    | 在新页面打开    |
| self      | 在当前页面打开   |
| _parent   | 在父框架中打开   |
| _top      | 在整个窗口中打开  |
| framename | 在指定的框架中打开 |

未指明时，默认为_self。

## 1.4 表单的同步提交及缺点

### 1.4.1 什么是表单的同步提交

通过点击 submit 按钮，触发表单提交的操作，从而是页面跳转到 action URL 的行为，叫做表单的同步提交。

### 1.4.2 表单同步提交的缺点

1. 表单同步提交后，整个页面会发生跳转，用户体验差。

2. 表单同步提交号，页面之前的状态和数据会丢失

### 1.4.3 如何解决表单同步提交的缺点

解决方案：表单只负责采集数据、Ajax负责将数据提交到服务器。

# 2. 通过Ajax提交表单数据

## 2.1 监听表单提交事件

```javascript
// 方式一
$.('#form1').submit(function(e){
    alert('监听了表单的提交事件！')
})
// 方式二
$.('#form1').on('submit', function(e){
    alert('监听了表单的提交事件！')
})
```

## 2.2 阻止表单默认提交行为

当监听到表单的提交事件后，可以调用事件对象的 event.preventDefault() 函数，来阻止表单的提交和页面的跳转。

```javascript
$.('#form').submit(function(e){
    alert('监听了表单的提交事件！')
    // 阻止表单的提交和页面的跳转
    e.preventDefault()
})

$.('#form').on('submit', function(e){
    alert('监听了表单的提交事件！')
    // 阻止表单的提交和页面的跳转
    e.preventDefault()
})
```

## 2.3 快速获取表单中的数据

**1、serialize() 函数**

为了简化表单中数据的获取操作，jQuery提供了serialize() 函数，其语法如下：

```javascript
$('#form').serialize()
```

serialize() 函数的好处：可以一次性获取到表单中的所有数据。

**2、serialize() 函数示例**

```html
<form id="form">
  <input type="text" name="username">
  <input type="password" name="password">
  <button type="submit">提交</button>
</form>
```

```javascript
$('#form').serialize()
// 调用的结果：
// userame=用户名的值&password=密码的值
```

注意：在使用 serialize() 函数快速获取表单数据时，必须为每个表单元素添加 name 属性。

# 3. 案例

## 3.1 基于bootstrap渲染评论列表的UI结构

## 3.2 获取并渲染评论列表

## 3.3 改造form表单&事项发表评论的功能

# 4. 模板引擎

## 4.1 渲染UI结构时遇到的问题

如果UI结构比较复杂，则拼接字符串时需要格外注意引号之前的嵌套，且一旦需求发生变化，修改起来也非常麻烦。

## 4.2模板引擎的概念

模板引擎，它可以根据程序员指定的模板结构和数据，自动生成一个完整的HTML页面。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-06-27-16-16-43-image.png)

## 4.3 模板引擎的好处

1. 减少了字符串的拼接操作

2. 使代码结构更清晰

3. 使代码更易于阅读维护

# 5. art-template 模板引擎

art-template 是一个简约、超快的模板引擎。

## 5.1 art-template 模板引擎的基本使用

**1、使用传统方式渲染UI结构**

```html
<div id="title"></div>
<div id="name"></div>
<div id="age"></div>


<script>
var data={
    title: '<h3>用户信息</h3>',
    name: 'jack',
    age: 18
}
$(function(){
    $.('title').html(data.title)
    $.('name').html(data.name)
    $.('age').html(data.age)
})
</script>
```

**2、art-template 的使用步骤**

1. 导入 art-template

2. 定义数据

3. 定义模板

4. 调用 template 函数

5. 渲染 HTML 结构

```html
<head>
    <!-- 1.导入art-template-->
    <script src="./template-web.js"></script>
    <script src="./jquery.js"></script>
</head>
<body>
    <div id="container"></div>

    <!-- 3.定义模板-->
    <script type="text/html" id="tpl">
        <p>{{name}}<p>
        <p>{{age}}<p>
    </script>

    <script>
        // 2.定义数据
        var data = {name: 'jack', age: 18}

        // 4.调用 template 函数
        var htmlStt = template('tpl',data)
        console.log(htmlStr)

        // 5.渲染 HTML 结构
        $.('#container').html(htmlStr)
    </script>
</body>
```

## 5.2 art-template 的标准语法

**1、输出**

```html
{{value}}
{{obj.key}}
{{a ? b: c}}
{{a || b}}
{{a + b}}
```

**2、原文输出**

如果要输出的 value 值中，包含了HTML标签结构，则需要使用原文输出语法，才能保证HTML标签被正常渲染。

```html
{{@ value}}
```

**3、条件输出**

```html
{{if 条件}}内容{{/if}}

{{if 条件一}}内容1
{{else if 条件二}}内容2
{{/if}}
```

**4、循环输出**

```html
{{each arr}}
    {{$index}}{{$value}}
{{/each}}
```

**5、过滤器**

```html
{{value | filterName}}


// 定义过滤器
template.defaults.imports,filterName = function(value){ return 返回的结果 }
```

# 6. 模板引擎的实现原理

## 6.1 正则与字符串操作

### 1、基本语法

exec() 函数用于检索字符串中的正则表达式的匹配。

如果字符串中有匹配的值，则返回该匹配值，否则返回 null。

```javascript
RegExpObject.exec(string)
```

示例代码如下：

```javascript
var str = 'hello'
var pattern = /o/

console.log(pattern.exec(str)
// 输出的结果["o", index: 4, input: "hello", groups: undefined]
```

### 2、分组

正则表达式中（）包起来的内容表示一个分组，可以通过分组来提取自己想要的内容，示例代码如下：

```javascript
var str = '<div>我是{{name}}</div>'
var pattern = /{{([a-zA-Z]+)}}/

var patternResult = pattern.exec(str)
console.log(patterResult)
// 得到 name 相关的分组信息
// ["{{name}}", "name", index: 7, input: "<div>我是{{name}}</div>", groups: undefined]
```

### 3、字符串的replace函数

replace() 函数用于在字符串中用一些字符替换另一些字符，语法格式如下：

```javascript
var result = '123456'.replace('123','abc')
// 得到的 result 字符串的值为 abc456
```

示例代码如下：

```javascript
var str = '<div>我是{{name}}</div>'
var pattern = /{{([a-zA-Z]+)}}/

var patternResult = pattern.exec(str)
str = str.replace(patternResult[0],patternResult[1])
//replace 函数的返回值为替换后的新字符串

console.log(str)
// 输出的内容是： <div>我是name</div>
```

### 4、多次replace

```javascript
var str = '<div>{{name}}今年{{age}}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

// 第一次匹配
var patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1])
console.log(str) // 输出< div>name今年{{age}}岁了</div>

// 第二次匹配
var patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1])
console.log(str) // 输出< div>name今年age岁了</div>

// 第三次匹配
var patternResult = pattern.exec(str）
console.log(str) // 输出 null
```

### 5、使用while循环replace

```javascript
var str = '<div>{{name}}今年{{age}}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = null
while(patternResult = pattern.exec(str)){
    str = str.replace(patternResult[0], patternResult[1])
}
console.log(str) // 输出 <div>name今年age岁了</div>
```

### 6、replace替换为真值

```javascript
var data = {name: 'jack', age: 18}
var str = '<div>{{name}}今年{{age}}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = null
while(patternResult = pattern.exec(str)){
    str = str.replace(patternResult[0], data[patternResult[1]])
}
console.log(str) // 输出 <div>jack今年18岁了</div>
```

## 6.2 实现简易的模板引擎

**实现步骤**

1. 定义模板结构

2. 预调用模板引擎

3. 封装 template 函数

4. 导入并使用自定义的模板引擎

**1、定义模板结构**

```javascript
<script type="text/html" id="tpl-user">
    <div>姓名：{{name}}</div>
    <div>年龄：{{ age }}</div>
    <div>性别：{{  gender}}</div>
    <div>住址：{{address}}</div>
</script>
```

**2、预调用模板引擎**

```javascript
<script>
    // 定义数据
    var data = {name: 'jack',age: 20, gender: '男', address: '北京海淀'}

    // 调用模板函数
    var htmlStr = template('tpl-user', data)

    // 渲染HTML结构
    document.getElementById('user-box').innnerHTML = htmlStr
</script>
```

**3、封装 template 函数**

```javascript
// .template.js文件中
function template(id,data){
    var str = document.getElementById(id).innerHTML
    var pattern = /{{\s*([a-zA-z]+)\s*}}/

    var patternResult = null

    while(patternResult = pattern.exec(str)){
        str = str.replace(patternResult[0], patternResult[1])
    }

    return str
}
```

**4、导入并使用自定义的模板引擎**

```html
<head>
    <script src="./template.js"></script>
</head>
<body>
    <div id="user-box"></div>

    <script type="text/html" id="tpl-user">
        <div>姓名：{{name}}</div>
        <div>年龄：{{ age }}</div>
        <div>性别：{{  gender}}</div>
        <div>住址：{{address}}</div>
    </script>

    <script>
        // 定义数据
        var data = {name: 'jack',age: 20, gender: '男', address: '北京海淀'}

        // 调用模板函数
        var htmlStr = template('tpl-user', data)

        // 渲染HTML结构
        document.getElementById('user-box').innnerHTML = htmlStr
    </script>
</body>
```
