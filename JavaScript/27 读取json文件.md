# 读取json文件

## fetch 方式

```js
var data = {}

fetch('./theme.json')
  .then((response) => response.json())
  .then((json) => {
    // console.log(json)
    data = json
}}
```

## ajax 方式

```js
$.ajax({
    url:'./theme.json',
    type:'get',
    dataType:'json',
    success: function(res){
        console.log(res)
        saveDate(res) // 通过回调函数来保存数据
    }
})


function saveData(res){
    data = res
}
```

## import 方式

- 在vue单组件中可以直接使用import导入json文件中的数据。

- 在html文件中，需要在 `script`标签中使用`type="module"`来表明类型，从而使用 `import` 语法。

html中

```html
<script type="module">
  import data from './theme.json' assert {type: 'json'}; // 指明导入类型
  console.log('import的json文件', data)
</script>
```

vue中

```
<script>
  import data from './theme.json' assert {type: 'json'};
  console.log('import的json文件', data)
</script>

<template>
</template>

<style>
</style>
```

**注意：** 在 `import` 导入 json 时，默认导入类型为 js，需要进行断言（assert），指明导入类型为 json。
