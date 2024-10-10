# electron 工作流程

## electron结构示意图

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2024-09-21-09-31-22-image.png)

一个 electron 应用由三部分组成：主进程、渲染进程、native apis。

### 主进程

- 可以看作是 package.json 中 main 属性对应的文件

- 一个应用只会有一个主进程

- 只有主进程可以进行 GUI 的 API 操作

### 渲染进程

- Windows 中展示的界面通过渲染进程表现

- 一个应用可以有多个渲染进程

## electron应用启动过程示意图

![](C:\Users\maxuanbo\AppData\Roaming\marktext\images\2024-09-21-09-32-29-image.png)

启动应用后，首先运行主进程创建窗口，然后渲染进程渲染窗口内容，最后给窗口内容绑定事件。 

当事件被触发时，渲染窗口做出反应，根据事件类型由渲染窗口处理，或者交给主进程进行处理。
