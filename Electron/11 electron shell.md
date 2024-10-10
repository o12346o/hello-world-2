# electron shell

使用默认应用程序管理文件和 url。

在主进程中

```js
const { shell } = require('electron')

ipcMain.on('show-item-in-foler', (e,fullPath) => {
  shell.showItemInFolder(fullPath)
}}

ipcMain.on('shell-url', () => {
  shell.openExternal('https://www.github.com')
})
```
