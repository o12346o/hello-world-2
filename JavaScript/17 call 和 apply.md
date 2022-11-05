#  call 和 apply

这两个方法都是函数对象的方法，需要通过函数对象来调用。

当函数调用 call() 和 appluy() 都会调用函数执行。

```js

function fun(){
    console.log(this)
}

fun.call();
fun.apply();
```

在调用 call() 和 apply() 时可以将一个对象指定为第一个参数，此时这个对象会成为函数执行时的 this。

```js
function fun(){
    console.log(this.name)
}

var obj = {name: 'tom'}
var obj2 = {name: 'obj2'}

fun.call(obj)
fun.call(obj2)
``` 

call() 方法可以将实参在对象之后依次传递，
apply() 方法可以将实参封装在一个数组内统一传递。

```js
function fun(x, y){
    console.log(this.name)
    console.log(x, y)
}

var obj = {name: 'tom'}
var obj2 = {name: 'obj2'}

fun.call(obj, 1, 2)
fun.apply(obj, [1, 2])
```

