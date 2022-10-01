# 1、安装Vue

## 1.1 CDN方式

开发版本

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.8/dist/vue.js"></script>
```

也可以使用生产版本（vue.min.js），体积更小。

## 1.2 npm方式

```powershell
npm install vue
```

## 1.3 直接下载Vue.js文件

vue.js 文件下载到本地后，script标签引入后，即可使用 vue。

# 2、Vue的介绍

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## 2.1 模板语法

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统：

```html
<div id="app">  
    {{ message }}  
</div>
```

```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

显示结果为：

```
Hello Vue!
```

## 2.2 条件与循环

### 2.2.1 v-if

```html
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>
```

```js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

渲染结果为：

```
现在你看到我了
```

### 2.2.2 v-show

```html
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>
```

```js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

渲染结果为：

```
现在你看到我了
```

### 2.2.3 v-if 和 v-show 的区别

v-if：如果条件不满足，则不会渲染元素，dom表中没有这个元素。

v-show：渲染元素，如果条件不满足，则不显示元素，dom表中有这个元素。

### 2.2.4 v-for


