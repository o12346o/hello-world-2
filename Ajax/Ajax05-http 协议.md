# 1、HTTP协议简介

## 1.1 什么是通信

通信，就是信息的传递和交换。

通信三要素：

- 通信的主体

- 通信的内容

- 通信的方式

## 1.2 什么是通信协议

通信协议是指通信的双方完成通信必须遵守的规则和约定。

通俗的理解：通信双方采用约定好的格式来发送和接收消息，这种事先约定好的通信格式，就叫做通信协议。

## 1.3 HTTP

**1、什么是HTTP协议**

HTTP 协议即超文本传送协议（Hyper Text Transfer Protocol），它规定了客户端与服务器之间进行网页内容传传输时，所必须遵守的传输格式。

**2、HTTP协议的交互模型**

HTTP 协议采用了 请求/响应 的交互模型。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-23-36-image.png)

# 2、HTTP请求

## 2.1 什么时HTTP请求消息

由于 HTTP 协议属性客户端浏览器和服务器之间的通信协议，因此，客户端发起的请求叫做 HTTP 请求，客户端发送到服务器端的消息，叫做 HTTP 请求消息。

注意：HTTP 请求消息又叫做 HTTP 请求报文。

## 2.2 HTTP请求消息的组成部分

HTTP 请求消息由请求行、请求头部、空行和请求体 4 个部分组成。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-27-39-image.png)

**1、请求行**

请求行由请求当时、URL 和 HTTP 协议版本 3 个部分组成，它们之间使用空格隔开。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-29-21-image.png)

**2、请求头部**

请求头部用来描述客户端的基本信息，从而把客户端相关的信息告知服务器。

请求头部由多行 键/值 对组成，每行的键和值之间用英文的冒号分隔。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-31-27-image.png)

**请求头字段**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-32-37-image.png)

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-33-23-image.png)

**3、空行**

最后一个请求头字段的后面是一个空行，通知服务器请求头部至此结束。

请求消息中的空行，用来分隔请求头部与请求体。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-35-31-image.png)

**4、请求体**

请求体中存放的，是要通过 POST 方式提交到服务器的数据。

注意：只有 POST 请求才有请求体，GET请求没有请求体。

# 3、HTTP响应

## 3.1 什么是HTTP响应消息

响应消息就是服务器响应给客户端的消息内容，也叫做响应报文。

## 3.2 HTTP响应消息的组成部分

HTTP响应消息由状态行、响应头部、空行 和 响应体 4 个部分组成。 ![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-40-13-image.png)

**1、状态行**

状态行由HTTP协议版本、状态码和状态码的描述文本 2 个部分组成，它们之间用空格隔开。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-42-19-image.png)

**2、响应头部**

响应头部用来描述服务器的基本信息。响应头部由多行 键/值 对组成。每行的键和值之间用英文的冒号分隔。

 ![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-43-53-image.png)

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-44-24-image.png)

**3、空行**

在最后一个响应头部字段结束之后，会紧跟一个空行，用来通知客户端响应头部至此结束。

响应消息中的空行，用来分隔响应头部与响应体。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-46-29-image.png)

**4、响应体**

响应体中存放的，是服务器响应给客户端的资源内容。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-47-22-image.png)

# 4、HTTP 请求方法

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-48-21-image.png)

# 5、HTTP响应状态代码

## 5.1 什么是HTTP响应状态码

HTTP响应状态码（HTTP Status Code），也是属于 HTTP 协议的一部分，用来标识响应的状态。

响应状态吗会随着响应消息一起被发送到客户端浏览器，浏览器根据服务器返回的响应状态码，就能知道这次 HTTP 请求的结果是成功还是失败。

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-51-23-image.png)

## 5.2 HTTP响应状态码的组成及分类

HTTP 状态码由三个十进制数字组成，第一个十进制数字定义了状态码的类型，后两个数字用来对状态码进行细分。

HTTP 状态码共分为 5 种分类：

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-53-34-image.png)

**2xx 成功相关的响应状态码**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-54-09-image.png)

**3xx 重定向相关的响应状态码**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-54-37-image.png)

**4xx 客户端错误相关的响应状态码**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-55-02-image.png)

**5xx 服务器端错误的相关的响应状态码**

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2022-07-11-15-55-30-image.png)
