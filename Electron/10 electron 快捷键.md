# electron 快捷键

## 本地快捷键

本地快捷键仅在应用聚焦时可用。

在`main.js`中，在menu上设置本地快捷键

```js
const menu = new Menu([
  { 
    label: '编辑'，
    submenu:[
      {
        label: '保存',
        accelerator: 'ctrl + s',
        click(){ console.log('保存‘) }
      }
    ]
  }
])
```

## 全局快捷键

使用`globalShortcut`来监测键盘事件

在`main.js`中

```js
const { globalShortcut } = require('electron')

app.whenReady().then(()=>{
  globalShortcut.register('ctrl + s', () => {
    console.log('全局键盘事件')
  })
}).then(createWindow)

app.on('close-window-all', () => {
  globalShortcut.unregisterAll()
})
```
