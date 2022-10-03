# 处理图片资源

**资源模块(asset module)** 是一种模块类型，它允许使用资源文件（字体，图标等）而无需配置额外 loader。

在 webpack 5 之前，通常使用：

- [`raw-loader`](https://v4.webpack.js.org/loaders/raw-loader/) 将文件导入为字符串
- [`url-loader`](https://v4.webpack.js.org/loaders/url-loader/) 将文件作为 data URI 内联到 bundle 中
- [`file-loader`](https://v4.webpack.js.org/loaders/file-loader/) 将文件发送到输出目录

**资源模块类型(asset module type)** ，通过添加 4 种新的模块类型，来替换所有这些 loader：

- `asset/resource` 发送一个单独的文件并导出 URL。之前通过使用 `file-loader` 实现。
- `asset/inline` 导出一个资源的 data URI。之前通过使用 `url-loader` 实现。
- `asset/source` 导出资源的源代码。之前通过使用 `raw-loader` 实现。
- `asset` 在导出一个 data URI 和发送一个单独的文件之间自动选择。之前通过使用 `url-loader`，并且配置资源体积限制实现。

## 1、resource 资源类型

---

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },
+ module: {
+   rules: [
+     {
+       test: /\.png/,
+       type: 'asset/resource'
+     }
+   ]
+ },
};
```

**src/index.js**

```js
import mainImage from './images/main.png';

img.src = mainImage; // '/dist/151cfcfa1bd74779aadb.png'
```

所有 `.png` 文件都将被发送到输出目录，并且其路径将被注入到 bundle 中，除此之外，你可以为它们自定义 [`outputPath`](https://webpack.docschina.org/configuration/module/#rulegeneratoroutputpath) 和 [`publicPath`](https://webpack.docschina.org/configuration/module/#rulegeneratorpublicpath) 属性。

### 自定义输出文件名

默认情况下，`asset/resource` 模块以 `[hash][ext][query]` 文件名发送到输出目录。

可以通过在 webpack 配置中设置 [`output.assetModuleFilename`](https://webpack.docschina.org/configuration/output/#outputassetmodulefilename) 来修改此模板字符串：

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
+   assetModuleFilename: 'images/[hash][ext][query]'
  },
  module: {
    rules: [
      {
        test: /\.png/,
        type: 'asset/resource'
      }
    ]
  },
};
```

另一种自定义输出文件名的方式是，将某些资源发送到指定目录：

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
+   assetModuleFilename: 'images/[hash][ext][query]'
  },
  module: {
    rules: [
      {
        test: /\.png/,
        type: 'asset/resource'
-     }
+     },
+     {
+       test: /\.html/,
+       type: 'asset/resource',
+       generator: {
+         filename: 'static/[hash][ext][query]'
+       }
+     }
    ]
  },
};
```

使用此配置，所有 `html` 文件都将被发送到输出目录中的 `static` 目录中。

`Rule.generator.filename` 与 [`output.assetModuleFilename`](https://webpack.docschina.org/configuration/output/#outputassetmodulefilename) 相同，并且仅适用于 `asset` 和 `asset/resource` 模块类型。

## 2、inline 资源类型

---

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
+       test: /\.svg/,
+       type: 'asset/inline'
     }
    ]
  }
};
```

**src/index.js**

```js
+ import metroMap from './images/metro.svg';

+ block.style.background = `url(${metroMap})`; // url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDo...vc3ZnPgo=)
```

所有 `.svg` 文件都将作为 data URI 注入到 bundle 中。

### 自定义 data URI 生成器

webpack 输出的 data URI，默认是呈现为使用 Base64 算法编码的文件内容。

如果要使用自定义编码算法，则可以指定一个自定义函数来编码文件内容：

**webpack.config.js**

```js
const path = require('path');
+ const svgToMiniDataURI = require('mini-svg-data-uri');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.svg/,
        type: 'asset/inline',
+       generator: {
+         dataUrl: content => {
+           content = content.toString();
+           return svgToMiniDataURI(content);
+         }
+       }
      }
    ]
  },
};
```

现在，所有 `.svg` 文件都将通过 `mini-svg-data-uri` 包进行编码。

## 3、source 资源类型

---

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
+       test: /\.txt/,
+       type: 'asset/source',
      }
    ]
  },
};
```

**src/example.txt**

```
Hello world
```

**src/index.js**

```js
+ import exampleText from './example.txt';

+ block.textContent = exampleText; // 'Hello world'
```

所有 `.txt` 文件将原样注入到 bundle 中。

## 4、asset 资源类型

---

又叫做通用性资源类型，根据资源大小来决定是 resource 还是 inline 资源。

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
+       test: /\.txt/,
+       type: 'asset',
      }
    ]
  },
};
```

现在，webpack 将按照默认条件，自动地在 `resource` 和 `inline` 之间进行选择：小于 8kb 的文件，将会视为 `inline` 模块类型，否则会被视为 `resource` 模块类型。

可以通过在 webpack 配置的 module rule 层级中，设置 [`Rule.parser.dataUrlCondition.maxSize`](https://webpack.docschina.org/configuration/module/#ruleparserdataurlcondition) 选项来修改此条件：

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.txt/,
        type: 'asset',
+       parser: {
+         dataUrlCondition: {
+           maxSize: 4 * 1024 // 设置转换界限为 4kb
+         }
+       }
      }
    ]
  },
};
```

还可以 [指定一个函数](https://webpack.docschina.org/configuration/module/#ruleparserdataurlcondition) 来决定是否 inline 模块。

## 小结

| 类型       | 打包后，是否有独立的文件 | 是否转换成 base64 格式 | 备注        |
| -------- |:------------:|:---------------:|:---------:|
| resource | 有            | 否               | 可自定义输出文件名 |
| inline   | 无            | 是               | 可自定义编码算法  |
| source   | 无            | 否               |           |
| asset    | 分情况          | 分情况             |           |

使用 base64 格式的意义：可以减少网络请求的次数。
