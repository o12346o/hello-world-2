# arguments

在调用函数时，浏览器每次都会传递两个隐含的参数：

- arguments 是一个类数组对象，它也可以通过索引来操作数据，也可以获取长度。

- 在调用函数时，传递的实参都会在 arguments 中保存。

- 即使不定义形参，也可以通过 arguments 来使用实参。

- 里面有一个属性，叫做 callee，对应一个函数对象，就是当前正在指向函数的对象。

```
function fun(){
    console.log(arguments instanceof Array)
    console.log(Array.isArray(arguments))
    console.log(arguments[1])
    console.log(arguments.length)
    console.log(arguments.callee == fun)
}

fun("hello",true);
```