# 浏览器计时器

用于测试业务代码的执行时间

```
// 开启计时器
console.time("计时器名"）

// 业务代码
for(var i = 1; i < 10 ; i++){
    console.log(i)
}

// 关闭计时器
console.timeEnd("计时器名")
```