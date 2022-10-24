# this

解析器在调用函数时，每次都会向函数内部传递进一个隐含的参数，

这个隐含的参数就是 `this` ，`this` 指向一个对象，

这个对象我们称为函数执行的**上下文对象**。

根据函数的调用方式不同，`this` 会指向不同的对象：

1. 以函数方式调用函数，this 指向 window。

2. 以对象方法方式调用函数，this 指向 对象。

```js
var name = "jack"
function fun(){
    console.log(this.name)
}
var obj = {
    name: "tom",
    sayName: fun
}
fun() // 打印 jack
obj.sayName // 打印 tom
```


