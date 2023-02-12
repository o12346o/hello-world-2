# background-size

当使用图片填充背景时，background-size 的不同值有不同的效果：

- cover：将图片保持宽高比，图片完全覆盖在背景中（背景满）

<img title="" src="file:///C:/Users/maxuanbo/AppData/Roaming/marktext/images/2023-02-12-19-50-32-image.png" alt="" width="464">

- contain：将图片保持宽高比，图片完全显示在背景中（背景可能为空）

<img title="" src="file:///C:/Users/maxuanbo/AppData/Roaming/marktext/images/2023-02-12-19-51-22-image.png" alt="" width="464">

- auto：图片保持原来尺寸

<img title="" src="file:///C:/Users/maxuanbo/AppData/Roaming/marktext/images/2023-02-12-19-51-57-image.png" alt="" width="463">

## 注意

 当 body 没有填满页面时，页面中会有空白（红框内为body）。

<img title="" src="file:///C:/Users/maxuanbo/AppData/Roaming/marktext/images/2023-02-12-19-52-33-image.png" alt="" width="455">

可以将设置`body{height:100%;width:100%}`使得body占满页面。需要注意的是：监听窗口滑动时，是 body 内元素相对 body 滑动而不是 body 相对窗口滑动。