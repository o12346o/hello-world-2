# Navigator

由于历史原因，Navigator 对象中的大部分属性已经不能帮助我们识别浏览器了。

一般我们只会使用 userAgent 来判断浏览器的信息，userAgent 是一个字符串，包含用来描述浏览器信息的内容，不同浏览器会有不同的 userAgent。

```js
console.log(navigator.userAgent)
```

- 火狐：Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:106.0) Gecko/20100101 Firefox/106.0

- 谷歌、edge、safari：Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.42

- ie10及以下：Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; Tablet PC 2.0; rv:11.0) like Gecko

- ie11：Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; Tablet PC 2.0)

```js
var ua = navigator.userAgent

console.log(ua)

if( /firefox/i.test(ua) ){
    alert("火狐")
}else if( /chrome/i.test(ua) ){
    alert("谷歌、Edge、safari")
}else if( /msie/i.test(ua){
    alert("ie8-10")
}else if( "ActiveXObject" in window){
    alert("ie11")
}
```