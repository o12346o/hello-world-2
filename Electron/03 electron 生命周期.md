# electron 生命周期

## 常用生命周期事件

1. ready：app 初始化完成【应用】

2. <mark>dom-ready</mark>：一个窗口中的dom加载完成【窗口】

3. <mark>did-finish-load</mark>：导航完成时触发【窗口】

4. <mark>closed</mark>：当窗口关闭时触发，此时应删除窗口引用【窗口】

5. window-all-closed：所有窗口都被关闭时触发【应用】

6. before-quit：在关闭窗口之前触发【应用】

7. will-quit：在窗口关闭并应用退出时触发【应用】

8. quit：当所有窗口被关闭时触发【应用】

**注**：还有其他生命周期事件未列出。

## 生命周期事件监听【代码示例】

主进程`main.js`中，使用`win.on()`和`app.on()`来监听事件

```js
const { app, BrowserWindow } = require('electron')

const creatWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600  
  })

  win.loadFile(index.html)

  win.on('dom-ready', () => {}) // 窗口dom准备完成
  win.on('did-finish-load', () => {}) // 窗口页面加载完成
  win.on('closed' , () => {}) // 窗口关闭后
}

app.whenReady().then(() => { creatWindow() }) // 应用加载完成，调用函数加载窗口
app.on('window-all-closed', () => { app.quit() }) // 所有窗口都关闭后,调用方法关闭应用
app.on('before-quit', () => {}) // 应用关闭前
app.on('will-quit', () => {}) // 将关闭应用
app.on('quit', () => {}) // 关闭应用



```
