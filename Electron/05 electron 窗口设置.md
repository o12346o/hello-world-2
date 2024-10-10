# electron 窗口设置

## 窗口尺寸、标题栏、菜单栏

在主进程`main.js`中：

- 可以设置窗口的尺寸

- 可以设置窗口的标题栏、菜单栏

```js
const win = new BrowserWindow({
  width: 800,
  height: 600,
  minHeight:400, // 设置窗口最大尺寸和最小尺寸
  maxWidth:1000,
  x: 10, // 窗口的起始位置（相对于屏幕左上角）
  y: 10,
  frame: true, // 设置是否显示框架，创建无边框窗口
  autoHideMenuBar: true, // 设置是否显示菜单栏
  maximizable: false, // 最大化和最小化窗口
  minimizable: true,
  icon: '0.ico', // 设置窗口图标
  title: '窗口', // 设置窗口标题，html中title中内容必须为空
  webPreferences: {
    preload: path.join(__dirname, 'preload.js')
  }
})
```

## 自定义窗口

在`main.js`设置隐藏默认标题栏

```js
const win = new BrowserWindow({
  width: 800,
  height: 600,
  titleBarStyle: 'hidden' , // 隐藏标题栏
  webPreferences: {
    preload: path.join(__dirname, 'preload.js')
  }
})


win.loadFile('index.html')
```

在`index.html`中准备好自己的标题栏

```js
<div id=‘myTitleBar’>
  <button id='minBtn'>最小化窗口</button>
  <button id='maxBtn'>最大化窗口</button>
  <button id='clsBtn'>关闭窗口</button>
</div>
```

在`preload.js`中暴露窗口操控方法（API）

```js
contextBridge.exposeInMainWorld('electronAPI', {
  minWin: () => ipcRenderer.send('minWin'),
  maxWin: () => ipcRenderer.send('maxWin'),
  closeWin: () => ipcRenderer.send('closeWin')
})
```

在`main.js`中设定监听

```js
ipcMain.on('minWin', () => {
  let currentWin = BaseWindow.getFocusedWindow() // 获取当前窗口
  currentWin.minimize()  // 窗口最小化
}}
// 注：最大化窗口和关闭窗口和以上类似，省略未显示
```

在渲染进程`index.js`中使用`preload.js`提供的API

```js
const minBtn = document.getElementById('minBtn')
const maxBtn = document.getElementById('maxBtn')
const clsBtn = document.getElementById('clsBtn')
minBtn.addEventListener('click', () => {
  window.electronAPI.minWin()
}) 
maxBtn.addEventListener('click', () => {
  window.electronAPI.maxWin()
}) 
clsBtn.addEventListener('click', () => {
  window.electronAPI.closeWin()
}) 
```

最终实现自定义窗口。

**注意**：隐藏默认标题栏后窗口不可以拖动，可以通过style设定来让窗口实现拖动。设置标题栏拖动，同时需要将按钮设置为非拖动，即可通过拖拽标题栏来实现窗口拖动。

```css
#myTitleBar {
    -webkit-app-region: drag;
}
#myTitleBar>button {
    -webkit-app-region: no-drag;
}
```
