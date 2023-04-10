# ejs03-.ejs文件

## 什么是 ejs 文件

以`.ejs`为后缀名的文件。例如：

【f2.ejs 文件中】

```ejs
<head>
    <title>ejs文件</title>
    <style><%- include("index.css") %></style>
</head>
```

## 使用 ejs 文件

### 在 ejs 文件中

使用`<%- include("ejs文件名") %>`来使用其他 `.ejs`文件。

【f1.ejs 文件中】

```ejs
<%- include("f2") %>
```

### 在 js 文件

使用renderFile()方法导入`.ejs`文件

```ejs
const ejs = require('ejs')
let html = ''

ejs.renderFile(filename,data,options,function(err,str){
    // str 为ejs文件中的内容，通过外部变量 html 保存到js文件中。
    html = str
})
```
