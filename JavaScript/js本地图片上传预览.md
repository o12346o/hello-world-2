# 本地图片上传预览

html中，上传图片

```html
<input type="file" onchange="loadFile(event)">
<br />
<img id="img" height="200px" />
```

js中，实现本地图片预览

```js
// 方式一：URL.createObjectURL方法
// createObjectURL是JS自带的一个函数，
// 它可以将Blob、File等二进制文件转为浏览器可直接显示的URL地址(即blob对象路径)
const loadFile = function (event) {
  const file = event.target.files[0] // 获取input上传的文件
  const blobUrl = window.URL.createObjectURL(file) // 得到blob对象路径
  console.log(blobUrl)
  const img = document.getElementById('img')
  img.src = blobUrl
}
```

```js
// 方式二： FileReader的readAsDataURL方法
// 用FileRader对像读取文件可分为四步；
// 1、创建FileReader对像；
// 2、调用readAsDataURL方法读取文件；
// 3、调用onload事件监听，我们一需要拿到完整的数据，
// 但我们又不知道文件何时读完，所以需要第三步监听；
// 4、通过FileRader对像r的result属性拿到读取结果。
const loadFile = function (event) {
  const file = event.target.files[0] // 获取input上传的文件
  const reader = new FileReader() // 创建FileRender对象
  reader.readAsDataURL(file) // 调用readAsDataURL()方法读取文件
  reader.onload = function () {
    const base64string = reader.result // 拿到读取结果
    const img = document.querySelector('#img')
    img.src = base64string
  }
}
```
