# 04 electron 进程间通信

electron默认开启沙盒模式。渲染进程不可以直接使用node、nativeApi进行操作。渲染进程不可以操作主进程，渲染进程之间也不可以直接通信。

## 开启非沙盒模式

在主进程`main.js`中，对指定的渲染进程开启非沙盒模式，通过`ipcMain`可以与渲染进程进行通信（监听渲染进程）

```js
// 其他代码省略未写
const win = new BrowserWindow({
  width: 800,
  height: 600,
  webPreferences: {
    contextIsolation: false, // 是否设置沙盒隔离模式，electron默认为沙盒模式
    nodeIntegration: true // 在渲染进程中是否可以使用node，必须在非沙盒模式下
  }
})

ipcMain.on('closeWin', () => { // 监听渲染进程发送过来的事件
  let curWin = BrowserWindow.getFocusWindow()
  // BrowserWindow.getFocusWindow() 获得当前窗口
  // 或者使用 BaseWindow.getFocusWinde() 也可以获得当前窗口
  curWin.close()
})
```

在渲染进程`index.js`中，可以使用node后，通过`ipcRenderer`与主进程进行通信

```js
const { ipcRenderer } = require('electron') // require是node语法

const btn = document.getElementById('btn')
btn.onClick() = function() {
  ipcRenderer.send('closeWin') // 将渲染进程中的事件发送给主进程
}
```

**注意**：为了安全性考虑，不建议使用非沙盒模式。渲染进程操作应该在DOM加载完成后，上述代码省略了这一部分。

## 使用预加载脚本，渲染进程向主进程发送消息（单向）

沙盒模式下，在主进程`main.js`中使用预加载脚本，预加载脚本在渲染进程加载前加载

使用`ipcMain.on()`可以监听渲染事件发送过来的消息

```js
const path = require('node:path') // 引入path模块，node:仅仅起标识作用

const win = new BrowserWindow({
  width: 800,
  height: 600,
  webPreferences: {
    preload: path.join(__dirname, 'preload.js') // 引入预加载脚本
  }
})

ipcMain.on('close-in', () => { // 监听渲染进程发送过来的事件
  let curWin = BaseWindow.getFocusWindow()
  curWin.close()
})
```

在预加载脚本`preload.js`中，使用`contextBridge`可以向渲染进程暴露有限的API

使用`ipcRenderer.send()`可以给主进程发送消息

```js
const { contextBridge, ipcRenderer } = require('electron')

// contextBridge可以暴露主进程中的API接口给渲染进程
contextBridge.exposeInMainWorld('electronAPI', { // electronAPI为自定义名称
  closeWin: () => ipcRenderer.send('closeWin')
})
```

在渲染进程 `index.js`中，使用`preload.js`暴露的API

```js
const btn = document.getElementById('btn')
btn.onClick() = function() {
  electronAPI.closeWin() // 使用electronAPI中的closeWin方法
}
```

## 渲染进程向主进程发消息（双向）

使用`ipcMain.handle()`和`ipcRenderer.invoke()`来双向发送消息。

在`main.js`中，`ipcMain.handle()`可以在监听的同时发送返回值

```js
async function handleFileOpen () { // 有返回值
  const { canceled, filePaths } = await dialog.showOpenDialog({})
  if (!canceled) {
    return filePaths[0]
  }
}

ipcMain.handle('openFile', handleFileOpen)
```

在`preload.js`中，`ipcRenderer.invoke()`可以在发送的同时接收返回值

```js
const { contextBridge, ipcRenderer } = require('electron')

contextBridge.exposeInMainWorld('electronAPI', {
  openFile: () => ipcRenderer.invoke('openFile')
})
```

在`index.js`中，

```js
const btn = document.getElementById('btn')
const filePathElement = document.getElementById('filePath')

btn.addEventListener('click', async () => {
  const filePath = await electronAPI.openFile() // 接收返回值
  filePathElement.innerText = filePath
})
```

## 主进程向渲染进程主动发送消息

在主进程`main.js`中，通过`webContents.send()`来实现主进程向渲染进程主动发送消息

```js
// 触发主进程中的点击事件后，通过webContents.send()发送消息给渲染进程
click: () => mainWindow.webContents.send('update-counter', 'value'),
```

在预加载脚本`preload.js`中，可以暴露API给渲染进程

```js
const { contextBridge, ipcRenderer } = require('electron')

contextBridge.exposeInMainWorld('electronAPI', {
  updateCounter: (callback) => ipcRenderer.on('update-counter', (e, val) => callback(val))// 接受主进程发送过来的消息，并调用回调函数
})
```

在渲染进程`index.js`中，使用暴露过来的API

```js
electronAPI.updateCounter((val) => { // 回调函数
  console.log(val)
})
```

## 主进程对渲染进程进行反馈

当渲染进程向主进程发送消息后，可以在主进程中对渲染进程进程反馈

在主进程中，通过`evnet.replay()`或`event.sender.send()`向渲染进程进行反馈

```js
ipcMain.on('counter-plus', (event, val) => { // 监听渲染进程
  let newVal = val + 1;
  event.sender.send('update-counter', newVal) } // 对渲染进程进行反馈
})
```

在`preload.js`中，暴露方式与 ”主进程向渲染进程主动发送消息“  的方式一样

```js
const { contextBridge, ipcRenderer } = require('electron')

contextBridge.exposeInMainWorld('electronAPI', {
  // 给主进程发送消息
  counterPlus: (val) => ipcRenderer.send('counter-plus',val) 
  // 接受主进程发送过来的消息，并调用回调函数
  updateCounter: (callback) => ipcRenderer.on('update-counter', (e, value) => callback(value)) 
})
```

在渲染进程`index.js`中，使用暴露过来的API

```js
let num = 1
electronAPI.counterPlus(num)
electronAPI.updateCounter((val) => { // 回调函数
  num = val
})
```

## 两个渲染进程之间进行通信，未完待续...

两个渲染进程之间的通信方式：

1. 使用`localStorage`来进行两个渲染进程之间的通信（只能传送字符串）

2. 通过主进程，来实现两个渲染进程之间的通信

3. 通过消息端口`MessagePort`，来实现两个渲染进程之间的通信
