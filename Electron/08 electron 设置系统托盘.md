# electron 设置系统托盘

在`main.js`中，使用`Tray`来设置系统托盘

```js
import { app, natvieImage, Menu, Tray } from "electron"

//创建托盘
const createTray = () => {
  //通过nativeImage.createFromPath()创建图标
  const icon = nativeImage.createFromPath('tray.png')

  // 创建系统托盘
  const tray = new Tray(icon) 

  // 创建菜单
  const contextMenu = Menu.buildFromTemplate([
    { label: '托盘'},
    { type: 'sperator'},
    { label: '退出', click(){ app.quit() } },
  ])

   // 将菜单附加到 tray 上
  tray.setContextMenu(menu)

  // 设置tray的双击事件
  tray.on('double-click', () => { win.show() })

  // 设置tray的toolTip
  tray.setToolTip('提示')
}

//当应用准备就绪后执行
app.whenReady().then(() => {
  createTray() //创建托盘
})
```
