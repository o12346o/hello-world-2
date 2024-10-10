# electron 自定义菜单

## 自定义菜单栏

在主进程`main.js`，使用`Menu()`来创建自定义菜单

```js
const { BroserWindow, Menu } = require('electron')
const path = require('node:path')

const win = new BrowserWindow({
  width: 800,
  height: 600,
  titleBarStyle: 'hidden' , // 隐藏标题栏
  webPreferences: {
    preload: path.join(__dirname, 'preload.js')
  }
})
win.loadFile('index.html')

// 设定菜单模板
let template = [
  { 
    lable: '编辑'，
    submenu: [
      {
        label: '复制',
        role: 'copy',
      },
      {
        label: '粘贴',
        role: 'paste'
      },
      { type: 'sperator'},
      {
        label: '保存',
        click: () => { console.log('save') }
      }
    ],
    {
      label: '关于'
    }
  }
]
// 根据模板创建菜单
let menu = Menu.buildFromTemplate(myMenu)
// 将菜单加载到应用上
Menu.setApplicationMenu(menu)
/* 或者
 * win.setMenu(menu)
 * 这样可以将menu设定为窗口（win）的菜单栏，而不是应用（app）的菜单栏
 */
```

## 自定义右键菜单

可以设定自定义右键菜单，使用`popup()`来弹出右键菜单

```js
// renderer.js（便于演示，未使用沙盒模式）
window.addEventListener('contextmenu', (e) => {
  e.preventDefault()
  ipcRenderer.send('show-context-menu')
})

  ipcRenderer.on('context-menu-command', (e, command) => {
  // ...
})

// main.js
ipcMain.on('show-context-menu', (event) => {
  const template = [
    {
      label: 'Menu Item 1',
      click: () => { event.sender.send('context-menu-command', 'menu-item-1') }
    },
    { type: 'separator' },
    { label: 'Menu Item 2', type: 'checkbox', checked: true }
  ]
  const menu = Menu.buildFromTemplate(template)
  menu.popup({ window: BrowserWindow.fromWebContents(event.sender) })
})
```

## 动态创建菜单

使用`new MenuItem()`可以创建菜单项，然后通过`Menu.append()`将菜单项添加到菜单中

```js
let menuItem1 = new MenuItem({
    label: 'one',
    submenu: []
})

let menu = new Menu()

menu.append(menuItem1) // 将菜单项添加到菜单中

Menu.setApplicationMenu(menu)
```

**注意：** 通过`Menu.getApplicationMenu()`得到的menu不支持动态添加或删除菜单项，但仍然可以动态修改**实例属性**`items`，或者通过重新设置应用菜单来实现添加和删除菜单项

```js
let menu = Menu.getApplicationMenu()

let menuItem2 = new MenuItem({
    label: 'two'
})

// 方式一
menu.append(menuItem2) // 不会动态修改应用的Menu
Menu.setApplicationMenu(menu) // 重新设置应用的Menu

// 方式二
menu.items[0].submenu.append(menuItem2) 
/** 需要注意的是:
  *    items 是一个数组
  *    items[0] 是一个菜单项
  *    items[0].submenu 才是一个菜单
  *    submenu 必须先有，才可以使用append()添加菜单项
  *    submenu 如果在items[0]中未写，则不可以用这个方法
  */
```
