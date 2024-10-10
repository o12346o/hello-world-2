# electron 对话框

在`main.js`中使用`dialog`设置对话框

```js
cocnst { dialog } = require('electron')

const creatDialog = function {
  dialog.showMessageBox({
    type: 'info',
    title: '通知',
    message: '对话框通知'
  })
}

ipcMain.on('open-dialog', () => {
  creatDialog()
})

ipcMain.handle('open-file', async () => {
  let res = await dialog.showOpenDialog({
    defaultPath: __dirname, // 设置默认打开路径
    title: '打开文件',
    buttonLabel: '选择', 
    properties: ['openFile', 'multiSelections'],
    filters: [ 
      // 设置文件过滤器，neme设定过滤器名称，extensions设定过滤文件类型
      { name: '代码文件', extensions: ['js', 'json', 'html'] },
      { name: '图片文件', extensions: ['jpg', 'jpeg', 'png'] },
      { name: '所有类型', extensions: ['*'] }
    ]
  })
  return res
})
```

在预加载脚本中

```js
const { contextBridge, ipcRenderer } = require('electron')

contextBridge.exposeInMainWorld('electronAPI', {
  oSend: (oName, value) => ipcRenderer.send(oName, value),
  oInvoke: (oName) => ipcRenderer.invoke(oName)
})
```

在渲染进程`index.js`中

```js
document.getElementById(btn').onclick = function() {
  electronAPI.oSend('open-dialog')
}

document.getElementById(open-file').onclick = function() {
  electronAPI.oInvoke('open-file').then(res => {
    console.log(res)
  })
}
```
