# ejs01入门

## 安装

利用 npm 安装 ejs 。

```bash
npm install ejs
```

## 用法

### 服务器端 或 Node环境中

 引入ejs，将 模板字符串 和 一些数据 作为参数传递给 ejs，即可生成 HTML 字符串。

```js
let ejs = require(ejs),
    people = ['geddy','neil','alex'],
    html  = ejs.render('<%= people.join(","); %>', {people: people});
```

其中，

`('<%= people.join(", "); %>`：为模板字符串，

`{people: people}`：为数据对象。

然后将生成的 HTML 字符串渲染到页面上即可。

```js
let body = document.body
let box = document.createElement('div')
box.innnerHTML = html
body.appendChild(box)
```

### 客户端（ejs不常用，不好用）

```html
<script src="ejs.js"></script>
<script>
  let people = ['geddy', 'neil', 'alex'],
      html = ejs.render('<%= people.join(", "); %>', {people: people});
      // 将 people 中的字符通过“,”连接成字符串。
</script>
```
