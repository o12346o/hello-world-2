# json

json 是字符串格式，其他语言可以识别；js 的 对象格式 只有 js 能识别，其他语言无法识别。

## json 和 对象 的相互转换

```js
var str = '{"name": "tom", "age": 18}'

console.log(str)
```

将json字符串转为对象

```js
var obj = JSON.parse(str) 

console.log(obj)
```

将对象转为json格式

```js
var str2 = JSON.stringify(obj)

console.log(str2)
```

## eval()

eval() 函数会将传入的字符串当做 JavaScript 代码进行执行。

```js
var obj2 = eval("(" + str + ")")

console.log(obj2)
```
