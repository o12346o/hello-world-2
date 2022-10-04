# 处理字体图标资源

字体图标不需要进行修改，原封不动使用即可。

在项目中，引入 iconfont.css 和 iconfont.ttf、iconfont.woff、iconfont.woff2。

## iconfont.css 文件中

```css
@font-face {
  font-family: "iconfont";
  /* Project id 3441355 */
  src: url('../fonts/iconfont.woff2') format('woff2'), 
    url('../fonts/iconfont.woff') format('woff'),
    url('../fonts/iconfont.ttf') format('truetype');
    /* url 根据具体情况进行修改 */
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-right:before {
  content: "\e683";
}

.icon-left:before {
  content: "\e684";
}

.icon-under:before {
  content: "\e685";
}

.icon-up:before {
  content: "\e686";
}

.icon-me:before {
  content: "\e6b1";
}

.icon-home:before {
  content: "\e6bc";
}

.icon-search:before {
  content: "\e6d4";
}
```

## 在 main.js 中使用 iconfont.css

```js
import 'iconfont.css'
```

## webpack.config.js 中修改配置

```js
+ {
+        test: /\.(ttf|woff2?)$/,
+        type: "asset/resource",
+        generator: { // 自定义输出目录
+          filename: 'static/medias/[hash:10][ext][query]' 
+        }
+ }
```

# 处理其他资源

如mp3、MP4、avi等，不需要进行进一步处理的资源，原封不动直接使用即可，也需要进行配置。

```js
{
-      /* test: /\.(ttf|woff2?)$/, */
       /* 直接添加需使用且不用处理的文件后缀即可 */
+      test: /\.(ttf|woff2?|mp3|mp4|avi)$/，
       type: "asset/resource",
        generator: { // 自定义输出目录
          filename: 'static/medias/[hash:10][ext][query]' 
        }
}
```
