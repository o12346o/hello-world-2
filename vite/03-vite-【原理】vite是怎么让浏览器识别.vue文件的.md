# 【原理】vite是怎么让浏览器识别.vue文件的？

vite 开启 服务器，

将 .vue 文件解析为 js 格式

通过设置 content-type 为 text/javascript，将解析后的文件发送到客户端。


