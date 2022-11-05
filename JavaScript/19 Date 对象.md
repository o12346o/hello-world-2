# Date 对象

## 创建时间对象

创建当前的时间对象

```js
var d = new Date()

console.log(d)
```

创建指定日期和时间的 Date 对象，需要在构造函数中传递一个表示时间的字符串作为参数

【日期格式】月/日/年 时:分:秒

```js
var d2 = new Date("11/05/2022 16:10:00")

console.log(d2)
```

## Date对象的方法

-getDate()：获取日

- getDay()：获取周几

- getMonth()：获取月份

- getFullYear()：获取年份

- getTime()：获取时间戳，从“标准时间1970年1月1日0时0分0秒”到“指定日期”的毫秒数。

- Date.now() 获取当前的时间戳，用来测试代码的性能。

- 等等。

```
var d2 = new Date()

var date = d2.getDate()
var day = d2.getDay()
var month = d2.getMonth() + 1
var year = d2.getFullYear()
var time = d2.getTime()

var start  = Date.now()

for(var i = 0; i < 10; i++){ // 测试代码 }

var end = Date.now()

console.log(end - start)
```
