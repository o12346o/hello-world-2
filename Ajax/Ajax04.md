# 1、了解同源策略和跨域

## 1.1 同源策略

**1、什么是同源**

如果两个页面的协议、域名和端口都相同，则两个页面具有相同的源。

**2、什么是同源策略**

同源策略（Same origin policy）是浏览器提供的一个安全功能。

同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。

通俗的理解：两个非同源页面之间，无法进行资源交互。例如：

1. 无法读取非同源网页的Cookie、Local Storage 和 IndexedDB

2. 无法接触非同源页面的DOM

3. 无法向非同源地址发送 Ajax 请求

## 1.2 跨域

**1、什么是跨域**

同源指的是两个URL的协议、域名、端口一致，反之，则是跨域。

**2、浏览器对跨域请求的拦截**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-11-38-51-image.png)

注意：浏览器允许发起跨域请求，但是，跨域请求回来的数据，会被浏览器拦截，无法被页面获取到。

**3、如何实现跨域数据请求**

两种解决方案：JSONP 和 CORS。

JSONP：出现的早，兼容性好。只支持GET请求，不支持POST请求。

CORS：出现的晚，W3C标准。支持GET和POST请求。不兼容某些低版本的浏览器。

# 2、JSONP

## 2.1 什么是JSONP

JSONP（JSON with Padding）是JSON的一种”使用模式“，可以哦那个有解决主流浏览器的跨域数据访问的问题。

## 2.2 JSONP的实现原理

由于浏览器同源策略，网页中无法通过 Ajax 请求非同源的接口数据。但是 script 标签不受浏览器同源策略的影响，可以通过 src 属性，请求非同源的 js 脚本。

JSONP 的实现原理：通过 script 标签的 src 属性，请求跨域的数据接口，并通过函数调用的形式，接收跨域接口响应回来的数据。

## 2.3 自己实现一个简单的JSONP

定义一个 success 回调函数：

```html
<script>
    function success(data){
    console.log('获取到了data数据！')
    console.log(data)
}
</script>
```

通过 script 标签，请求接口数据：

```html
<script src="http://www.baidu.com?callback=success&name=zs&age=18"></script>
```

## 2.4 JSONP的缺点

由于 JSONP 是通过 script 标签的 src 属性，来实现跨域数据获取的，所以，JSONP 只支持 GET 数据请求，不支持 POST 请求。

注意：JSONP 和 Ajax 之间没有任何关系，JSONP 没有用到 XMLHttpRequest 这个对象。

## 2.5 jQuery中的JSONP

jQuery 提供的 $.ajax() 函数，除了可以发起真正的 Ajax 数据请求之外，还能够发起 JSONP 数据请求：

```javascript
$.ajax({
    url: 'http://www.baidu.com?name=zs&age=20',
    // 如果要使用 $.ajax() 发起 JSONP 请求，必须指定 datatype 为 jsonp
    dataType: 'jsonp',
    success: function(res){
        console.log(res)
    }
})
```

默认情况下，使用 jQuery 发起 JSONP 请求，会自动携带一个 callback=jQueryxxx 的参数，jQueryxxx 是随机生成的一个回调函数名称。

## 2.6 自定义参数及回调函数名称

在使用 jQuery 发起 JSONP 请求时，如果想要自定义 JSONP 的参数及回调函数名称，可以通过如下两个参数来指定：

```javascript
$.ajax({
    url: 'http://www.baidu.com?name=zs&age=20',
    dataType: 'jsonp',
    // 发送到服务器端的参数名称，默认值为 callback
    jsonp: 'callback',
    // 自定义回调函数名称，默认值为 jQueryxxx 格式
    jsonpCallback: 'abc',
    success: function(res){
        console.log(res)
    }
})
```

## 2.7 jQuery中JSONP的实现过程

jQuery 中的 JSONP，也是通过 script 标签的 src 属性实现跨域数据访问的，只不过，jQuery 采用的是动态创建和移除 script 标签的方式，来发起数据JSONP请求。

- 在发起 JSONP 请求的时候，动态向 header 标签中 append 一个 script 标签；

- 在 JSONP 清除成功以后，动态从 header 标签中 移除刚才 append 进去的 script 标签。

# 3、案例-淘宝搜索

# 4、防抖和节流
