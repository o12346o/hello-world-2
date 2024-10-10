# electron 消息通知

## 渲染进程进行通知

可以直接使用渲染进程进行消息通知

在`index.html`中

```js
<button id='noti'>打开消息通知</button>
```

在`index.js`中

```js
window.onload = function(){
  let obtn = document.getElementById('noti')

  obtn.onclick = function(){
    // 消息通知配置
    let option = {
      title: '消息通知',
      body: '这是一条消息',
      icon: '0.png'
    }

    // 创建消息通知
    let myNotification = new window.Notification(option.title, option)

    // 消息通知被点击后
    myNotification.onclick = function(){
      console.log('点击了消息通知')
      // 后续操作
    }
  }

}
```

## 主进程进行通知

在`main.js`中，使用`Notification`进行通知

```js
import { Notification } from "electron"

//发送通知
ipcMain.handle("sendNotify", async () => {
    const notify = new Notification({ // 创建通知
        icon:"notify.ico", 
        title:"邓瑞编程",
        body:"dengruicode.com"
    })

    notify.show() // show()显示通知
})
```

在`preload.js`中

```js
contextBridge.exposeInMainWorld('electronAPI', {
  invoke: (oName) => ipcRenderer(oName)
})
```

在`index,js`中

```js
//发送通知
document.querySelector('#sendNotify').addEventListener('click', () => {
    electronAPI.invoke("sendNotify")
})
```
