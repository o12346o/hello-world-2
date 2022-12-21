# vite对css的处理

vite 天生就支持对 css 文件的直接处理

1. 读取 main.js 中引用了 index.css

2. 直接使用 fs 模块读取 index.css 中的内容

3. 创建一个 style 标签，将 index.css 中内容直接复制到 syle 标签里

4. 将 style 标签插入 index.html 文件的 head 中

5. 将该 css 文件中的内容直接替换为 js 脚本（方便热更新或css模块化），同时设置 content-type 为 js，从而让浏览器以 js 脚本的形式来执行该 css 后缀的文件。

## 【原理】

基于 node：

1. module.css（表示需要开启 css 模块化）

2. 他会将你的所有类名进行一定规则的替换（将 footer 替换成 _footer_123st_1）

3. 同时创建一个映射对象（footer: "_footer_123st_1"）

4. 将替换过后的内容塞进 style 标签里面然后放入到 head 标签中

5. 将 componentA.module.css 内容进行全部抹除，替换成 js 脚本

6. 将创建的映射对象在脚本中进行默认导出

## vite 配置文件中 css 的配置流程（modules 篇）

在 vite.config.js 中通过 css 属性去控制整个 vite 对 css 的处理行为。

- `localConvention`：修改生成的配置对象的 key 的展示形式（驼峰还是划线形式）

- `scopeBehaviour`：配置当前的模块化行为是模块化还是全局化（有 hash 就是开启模块化的一个标志）

- `generateScopedName`：生产类名的规则（可以配置为函数，也可以配置成字符串）

- `hashPrefix`：生成 hash 会根据你的类名进行生成，如果想要你生成的 hash 更独特一点，可以配置 hashPrefix，你配置的这个字符串会参与到最终的 hash 生成。

- `globalModulePaths`: 代表你不想参与 css 模块化的路径

vite.config.js 文件中：

```js
export default defineConfig({ /* 配置代码书写位置 */})
```

css 配置：

```js
css: { // 对css的行为进行配置
    modules: { // 对css模块化的默认行为进行配置
        localsConvention: "camelCase", // 修改生成的配置对象的 key 的展示形式（驼峰还是划线形式）
        scopeBehaviour: "local", // 开启模块化
        // generateScopeName: "{name}_{local}_{hash:10}",
        generateScopeName: (name, filename, css)=>{
            // name，代表的是当前 css 文件中的类名
            // filename，是当前 css 文件的绝对路径
            // css,是当前 css 文件的格式
            console.log(name, filename, css) // 会打印在node端
            // 配置成函数以后，返回值就绝对了最终显示的类型
            return `${name}_${Math.random().toString(36).substr(3,8)}`
        },
        hashPrefix: '123',
        globalModulePaths: ['./componentB.module.css'] // 指明不进行 css 模块化的路径
    }
}  
```

## vite 配置文件中 css 的配置流程（preprocessorOptions 篇）

主要是用来配置 css 预处理的一些全局参数：

```js
css: { // 对css的行为进行配置
    modules: { // 对css模块化的默认行为进行配置
    },
    preprocessorOptions: { // key + config，key代表预处理器的名字
        less: { // 整个的配置对象最终给到 less 的执行参数（全局参数）中去
            math: "always",
            globalVars: { // 配置全局变量
                mainColor: red
            }
        },
        sass: {

        }
    }
}  
```

less 单独使用示例：

```bash
npm i less # 安装 lessc 编译器

# 使用 lessc 将 .less 文件转为 .css 文件
npx lessc index.less
npx lessc --math="always" index.less # --math="always" 为执行参数（全局参数）
```

## devSourceMap

```js
css: { // 对css的行为进行配置
    modules: { // 对css模块化的默认行为进行配置
    },
    preprocessorOptions: { // 预处理器配置
    },
    devSourceMap:true // 配置是否开启 css 源码位置映射
}  
```

## postcss

vite 默认可用 postcss。

### postcss的作用

1. 语法降级：将高版本的css转为低版本css

2. 前缀补全（匹配不同的浏览器）

3. postcss 可以直接处理 less 和 sass 文件，然而，现在，postcss 更多的是作为后处理器（对 less、sass 处理完成后的 css 文件，再处理）

post.config.js文件中

```js
const postcssPresetEnv = require("postcss-preset-env")
// 预设环境里面是会包含很多的插件
// 语法降级(postcss-low-level)、编译插件(postcss-compiler)、等等...
module.exports = {
    plugins: [postcssPresetEnv()]
}
```

## vite 配置文件中 css 的配置流程（postcss 篇）

```js
css: { // 对css的行为进行配置
    modules: { // 对css模块化的默认行为进行配置
    },
    preprocessorOptions: { // 预处理器配置
    },
    devSourceMap:true, // 配置是否开启 css 源码位置映射
    postcss: {
        plugins: [postcssPresetEnv]
    }
}  
```

例如，在less文件中：

```less
.content{
    width: 400px;
    .main{
        width: clamp(100px, 30%, 200px) /* 百分之三十，最小100px，最大200px */
        /* post-preset-env 会对上面的代码进行降级 */
    }
}
```

postcss也可以在单独的配置文件（post.config.js）中进行配置，在 vite.config.js 中的配置的优先级高于 post.config.js 文件中的配置的优先级。

## 将全局变量放在一个单独的 css 文件中

variable.css 文件中

```css
:root{
    bgColor: red;
}
```

配置文件 postcss.config.js 中：

```js
const postcssPresetEnv = require("postcss-preset-env")
const path = require("path")

module.exports = {
    plugins: [
        postcssPresetEnv({
            importFrom: path.resolve(__dirname, "./variable.css"), // 告诉postcss，让一些全局变量记下来。
        })
   ]
}  
```


