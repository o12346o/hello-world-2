# 1、js简介

JavaScript 是脚本语言。

JavaScript 是一种轻量级的编程语言。

JavaScript 是可插入 HTML 页面的编程代码。

JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。

## js的作用

- 直接写入html输出流
  
  ```js
  document.write('输出内容');
  ```

- 对事件做出反应
  
  ```html
  <button onclick="alert(点击了)">按钮</button>
  ```

- 改变html的内容
  
  ```js
  const box = document.getElementById('demo');
  box.innerHTML = '<h1>hello！</h1>';
  ```

- 改变图像
  
  ```html
  <img src="/images/1.jpg" />
  <script>
      const img = document.querySelector('img');
      img.onclick = function(){
          img.src = '/images/2.jpg';
      }
  </script>
  ```

- 改变 HTML 元素的样式，属于改变 HTML 属性的变种。
  
  ```js
  const box = document.getElementById('demo');
  box.style.color = '#f00';
  ```

- 验证输入
  
  JavaScript 常用于验证用户的输入。
  
  ```js
  if isNaN(x) { 
      alert("不是数字"); 
  }
  
  if(isNaN(x) || x.replace(/(^\s*)|(\s*$)/g,"") == ""){
   alert("不是数字");
   }
  ```

# 2、js输出

## 2.1  弹出警告框

```js
window.alert();
```

## 2.2 写入HTML文档

```js
document.write();
```

注意：如果在文档已完成加载后执行 document.write，整个 HTML 页面将被覆盖。

## 2.3 操作HTML元素

```js
const box = document.getElementById('demo');
box.innerHTML = '<h1>hello！</h1>';
```

## 2.4打印到控制台

```js
console.log();
```

# 3、js语法

- 变量
  - var
  - let
  - 必须以字母开头，或$和_开头（不推荐），大小写敏感
- 字面量
  - 数字Number
  - 字符串String
  - 数组Array
  - 对象Object
  - 函数function
- 对大小写敏感
- 使用Unicode字符集

# 4、js数据类型

## 4.1 基本类型（值类型）

- 字符串 String

- 数字 Number

- 布尔 Boolean

- 空 null

- 未定义 undefined

- 标志 symbol 

## 4.2 对象类型（引用数据类型）

- 对象 Object

- 数组 Array

- 函数 Function

- 正则 RegExp

- 日期 Date

## 4.3 查看数据类型

### 4.3.1 typeof 查看基本数据类型

判断变量为何种基本数据类型，typeof 返回值为字符串。

```js
typeof “jack”;                   // 返回 String
typeof 3.14;                     // 返回 Number
typeof false;                    // 返回 Boolen
typeof [1,2,3];                  // 返回 Object
typeof {name: 'jack', age: 18};  // 返回 Object
```

### 4.3.2 instanceof

判断实例是否在对象原型链中，返回值为布尔值。

```js
var obj = {}
'jack' instanceof String    // 返回值为 true
[1,2,3] instanceof String   // 返回值为 false
[1,2,3] instanceof Array    // 返回值为 true
[1,2,3] instanceof Object    // 返回值为 true
{name: jack} instanceof Object    // 返回值为 true
obj instanceof Object    // 返回值为 true
```

### 4.3.3 Object.prototype.toString.call()

Object.prototype.toString.call() 或 Object.prototype.toString.apply()，返回值为[objcet Xxx]。

toString() 是 Object 的原型方法，调用该方法，默认返回当前对象的 [[Class]] 。这是一个内部属性，其格式为 [object Xxx] ，其中 Xxx 就是对象的类型。

对于 Object 对象，直接调用 toString()  就能返回 [object Object] 。而对于其他对象，则需要通过 call / apply 来调用才能返回正确的类型信息。

```js
var arr  = [1,2,3]
var str  = 'hello'
console.log(Object.prototype.toString.call(arr)) // 返回值为[object Array]
console.log(Object.prototype.toString.apply(arr)) // 返回值为[object Array]
console.log(Object.prototype.toString.apply(str)) // 返回值为[object String]
```

### 4.3.4 使用 constructor 属性

**constructor** 属性返回所有 JavaScript 变量的构造函数。

constructor 判断方法跟 instanceof 相似,但是 constructor 检测 Object与instanceof 不一样, constructor 还可以处理基本数据类型的检测,不仅仅是对象类型。

注意:

1.null 和 undefined 没有 constructor；

2.判断数字时使用(),比如  (123).constructor,如果写成123.constructor会报错；

3.constructor 在类继承时会出错,因为 Object 被覆盖掉了,检测结果就不对了。

```js
var str = ’hello‘;
var num  = 123;
console.log(str.constructor);
console.log((123).constructor); // 判断数字类型时需要用小括号包裹起来
console.log(num.constructor);
```

### 4.3.5 使用jquery.type()

必须在引用jquery后才能使用这个方法，非js原生方法，不常用。

```js
console.log(jquery.type('hello')) // 返回值为字符串“String”
console.log(jquery.type(123)) // 返回值为字符串“Number”
console.log(jquery.type(undifined)) // 返回值为字符串“undifined”
```

## 4.4 声明变量类型

### 4.4.1 赋值时自动声明变量类型

```js
var a;      // 变量类型为undefined
a = 18;     // 变量类型为Number
a = 'hello' // 变量类型自动变为为String
```

### 4.4.2 使用关键字new

可以使用关键字 “new” 来声明变量类型，使用new之后都是对象类型：

```js
var name = new String;
var x = new Number;
var t = new Boolen;
var cars = new Array;
var person = new Object;
```

# 5、 js对象

javaScript 对象是拥有属性和方法的数据。

## 5.1 对象定义

```js
var person = {
    firstName:"John",
    lastName:"Doe",
    age:50,
    eyeColor:"blue"
};
```

## 5.2 对象属性

键值对在 JavaScript 对象通常称为 **对象属性**。

访问对象属性，有两种方式：

```js
person.lastName;
```

或

```js
person["lastName"];
```

## 5.3 对象方法

对象的方法定义了一个函数，并作为对象的属性存储。

对象方法通过添加 () 调用 (作为一个函数)。

访问对象方法：

```js
objectName.methodName()
```

通常 fullName() 是作为 person 对象的一个方法， fullName 是作为一个属性。

如果使用 fullName 属性，不添加 **()**, 它会返回函数的定义：

```js
objectName.methodName
```

# 6、 js函数

```js
var a; // 全局变量
function 函数名(){
    var b; // 局部变量
    函数体
}
```

```js
const box = document.querySelector('#box')
box.onclick = function(){
    alert.log('点击了！')
}
```

# 6.1 作用域

局部变量会在函数运行以后被删除。

全局变量会在页面关闭后被删除。

# 7、js事件

事件可以用于处理表单验证，用户输入，用户行为及浏览器动作:

- 页面加载时触发事件
- 页面关闭时触发事件
- 用户点击按钮执行动作
- 验证用户输入内容的合法性
- 等等 ...

可以使用多种方法来执行 JavaScript 事件代码：

- HTML 事件属性可以直接执行 JavaScript 代码
- HTML 事件属性可以调用 JavaScript 函数
- 你可以为 HTML 元素指定自己的事件处理程序
- 你可以阻止事件的发生。
- 等等 ...

### 常见的HTML事件

| 事件          | 描述        |
| ----------- | --------- |
| onclick     | 点击事件      |
| onchange    | html 元素改变 |
| onmouseover | 鼠标移动到     |
| onmouseout  | 鼠标移走      |
| onkeydown   | 键盘按下      |
| onload      | 页面加载完成后   |

# 8、js字符串

符串可以是插入到引号中的任何字符。你可以使用单引号或双引号。

```js
const str = "hello"
const str = 'hello'
```

## 8.1 字符串可以是对象

通常， JavaScript 字符串是原始值，可以使用字符创建： **var firstName = "John"**

但我们也可以使用 new 关键字将字符串定义为一个对象： **var firstName = new String("John")**

```js
var x = "John";
var y = new String("John");
typeof x // 返回 String
typeof y // 返回 Object
```

不要创建 String 对象。它会拖慢执行速度，并可能产生其他副作用。

## 8.2 字符串的属性

| 属性          | 描述            |
| ----------- | ------------- |
| constructor | 返回创建字符属性的函数   |
| length      | 返回字符串的长度      |
| prototype   | 允许您向对象添加属性和方法 |

## 8.3 字符串方法

| 方法                 | 描述                                    |
| ------------------ | ------------------------------------- |
| chatAt()           | 返回索引位置的字符                             |
| charCodeAt()       | 返回索引位置字符的Unicode值                     |
| concat()           | 连接两个或多个字符串，返回新字符串                     |
| fromCharCode()     | 把Unicode转换为字符串                        |
| indexOf()          | 返回字符第一次出现位置                           |
| lastIndexOf()      | 返回字符最后一次出现位置                          |
| match()            | 找到一个或多个正则表达式的匹配                       |
| replace()          | 替换与正则表达式相匹配的值                         |
| search()           | 检索与正则表达式相匹配的值                         |
| slice()            | 提前字符串的片段，并在返回新字符串；</br> 在字符串指定位置插入字符。 |
| split()            | 把字符串分割为数组                             |
| substr()           | 从索引位置提前指定数目的字符                        |
| substring()        | 从两个指定的索引号之间提前字符                       |
| toLocalLowerCase() | 根据本地语言环境，转为小写                         |
| toLocalUpperCase() | 根据本地语言环境，转为大写                         |
| toLowerCase()      | 转为小写                                  |
| toUpperCase()      | 转为大写                                  |
| toString()         | 返回字符串对象值                              |
| trim()             | 移出字符串首尾空白                             |
| valueOf()          | 返回莫格字符串对象的原始值                         |

字符串与其他类型相加，实际上是进行了字符串拼接，结果为字符串。

# 9、js类型转换

在 JavaScript 中有 6 种不同的数据类型：

- string
- number
- boolean
- object
- function
- symbol

3 种对象类型：

- Object
- Date
- Array

2 个不包含任何值的数据类型：

- null
- undefined

## 9.1 typeof 操作符

可以使用 **typeof** 操作符来查看 JavaScript 变量的数据类型。

```js
typeof "John"                 // 返回 string
typeof 3.14                   // 返回 number
typeof NaN                    // 返回 number
typeof false                  // 返回 boolean
typeof [1,2,3,4]              // 返回 object
typeof {name:'John', age:34}  // 返回 object
typeof new Date()             // 返回 object
typeof function () {}         // 返回 function
typeof myCar                  // 返回 undefined (如果 myCar 没有声明)
typeof null                   // 返回 object
```

请注意：

- NaN 的数据类型是 number
- 数组(Array)的数据类型是 object
- 日期(Date)的数据类型为 object
- null 的数据类型是 object
- 未定义变量的数据类型为 undefined

如果对象是 JavaScript Array 或 JavaScript Date ，我们就无法通过 **typeof** 来判断他们的类型，因为都是 返回 object。

## 9.2 constructor 属性

**constructor** 属性返回所有 JavaScript 变量的构造函数。

```js
"John".constructor                 // 返回函数 String()  { [native code] }
(3.14).constructor                 // 返回函数 Number()  { [native code] }
false.constructor                  // 返回函数 Boolean() { [native code] }
[1,2,3,4].constructor              // 返回函数 Array()   { [native code] }
{name:'John', age:34}.constructor  // 返回函数 Object()  { [native code] }
new Date().constructor             // 返回函数 Date()    { [native code] }
function () {}.constructor         // 返回函数 Function(){ [native code] }
```

你可以使用 constructor 属性来查看对象是否为数组 (包含字符串 "Array"):

```js
function isArray(myArray) {
    return myArray.constructor.toString().indexOf("Array") > -1;
}
```

可以使用 constructor 属性来查看对象是否为日期 (包含字符串 "Date"):

```js
function isDate(myDate) {
    return myDate.constructor.toString().indexOf("Date") > -1;
}
```

## 9.3 JavaScript 类型转换

JavaScript 变量可以转换为新变量或其他数据类型：

- 通过使用 JavaScript 函数
- 通过 JavaScript 自身自动转换

### 9.3.1 将数字转换为字符串

全局方法 **String()** 可以将数字转换为字符串。

该方法可用于任何类型的数字，字母，变量，表达式：

```js
String(x)         // 将变量 x 转换为字符串并返回
String(123)       // 将数字 123 转换为字符串并返回
String(100 + 23)  // 将数字表达式转换为字符串并返回
```

Number 方法 **toString()** 也是有同样的效果。

```js
x.toString()
(123).toString()
(100 + 23).toString()
```

在 Number 方法中，你可以找到更多数字转换为字符串的方法:

| 方法              | 描述                         |
| --------------- | -------------------------- |
| toExponential() | 把对象的值转换为指数计数法。             |
| toFixed()       | 把数字转换为字符串，结果的小数点后有指定位数的数字。 |
| toPrecision()   | 把数字格式化为指定的长度。              |

### 9.3.2 将布尔值转换为字符串

全局方法 **String()** 可以将布尔值转换为字符串。

```js
String(false)        // 返回 "false"  
String(true)         // 返回 "true"
```

Boolean 方法 **toString()** 也有相同的效果。

```js
false.toString()     // 返回 "false"  
true.toString()      // 返回 "true"
```

### 9.3.3 将日期转换为字符串

Date() 返回字符串。

```js
Date()      // 返回 Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)
```

全局方法 String() 可以将日期对象转换为字符串。

```js
String(new Date())      // 返回 Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)
```

Date 方法 **toString()** 也有相同的效果。

```js
obj = new Date()  
obj.toString()   // 返回 Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)
```

### 9.3.4 将字符串转换为数字

全局方法 **Number()** 可以将字符串转换为数字。

字符串包含数字(如 "3.14") 转换为数字 (如 3.14).

空字符串转换为 0。

其他的字符串会转换为 NaN (不是个数字)。

```js
Number("3.14")    // 返回 3.14  
Number(" ")       // 返回 0  
Number("")        // 返回 0  
Number("99 88")   // 返回 NaN
```

在 Number 方法中，你可以查看到更多关于字符串转为数字的方法：

| 方法           | 描述                |
| ------------ | ----------------- |
| parseFloat() | 解析一个字符串，并返回一个浮点数。 |
| parseInt()   | 解析一个字符串，并返回一个整数。  |

### 9.3.5 一元运算符 +

**Operator +** 可用于将变量转换为数字：

```js
var y = "5";      // y 是一个字符串  
var x = + y;      // x 是一个数字
```

如果变量不能转换，它仍然会是一个数字，但值为 NaN (不是一个数字):

```js
var y = "John";   // y 是一个字符串  
var x = + y;      // x 是一个数字 (NaN)
```

### 9.3.6 将布尔值转换为数字

全局方法 **Number()** 可将布尔值转换为数字。

```js
Number(false)     // 返回 0  
Number(true)      // 返回 1
```

### 9.3.7 将日期转换为数字

全局方法 **Number()** 可将日期转换为数字。

```js
d = new Date();  
Number(d)          // 返回 1404568027739
```

日期方法 **getTime()** 也有相同的效果。

```js
d = new Date();  
d.getTime()        // 返回 1404568027739
```

### 9.3.8 自动转换类型

当 JavaScript 尝试操作一个 "错误" 的数据类型时，会自动转换为 "正确" 的数据类型。

以下输出结果不是你所期望的：

```js
5 + null    // 返回 5         null 转换为 0  
"5" + null  // 返回"5null"   null 转换为 "null"  
"5" + 1     // 返回 "51"      1 转换为 "1"
"5" - 1     // 返回 4         "5" 转换为 5
```
