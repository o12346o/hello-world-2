# Location 对象

获取当前页面的地址

```js
console.log(location)
```

跳转到指定页面（在当前页面中进行跳转）

```js
location = "https://www.baidu.com" // 相对地址或绝对地址。
// 或
location.href = "https://www.baidu.com"
```

会在 history 中添加历史记录。

## 属性

| 属性       | 描述                   |
| -------- | -------------------- |
| hash     | 设置或返回从#开始的 URL       |
| host     | 设置或返回主机名和当前 URL 的端口号 |
| hostname | 设置或返回当前 URL 的主机名     |
| href     | 设置或返回完整的 URL         |
| pathname | 设置或返回当前 URL 的路径部分    |
| port     | 设置或返回当前 URL 的端口号     |
| portcool | 设置或返回当前 URL 的协议      |
| search   | 设置或返回从？开始的URL（查询部分）  |

## 方法

| 属性        | 描述                               |
| --------- | -------------------------------- |
| assign()  | 加载新的文档，和直接修改location一样。          |
| reload()  | 重新加载当前文档。如果传入一个参数 true，则会强制刷新页面。 |
| replace() | 用新的文档替换当前文档。不会生成历史记录。            |

## 打开新页面

```js
window.open("https://www.baidu.com") // 会在新的标签页打开
```