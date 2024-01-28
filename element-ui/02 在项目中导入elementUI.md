# 在项目中导入elementUI

## 完整引入

```js
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)

app.use(ElementPlus)
app.mount('#app')
```

## 按需引入

您需要使用额外的插件来导入要使用的组件。

#### 自动导入

首先你需要安装`unplugin-vue-components` 和 `unplugin-auto-import`这两款插件

```
npm install -D unplugin-vue-components unplugin-auto-import
```

然后把下列代码插入到你的 `Vite` 或 `Webpack` 的配置文件中

```js
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  // ...
  plugins: [
    // ...
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```

### 手动导入

Element Plus 提供了基于 ES Module 的开箱即用的 [Tree Shaking](https://webpack.js.org/guides/tree-shaking/) 功能。

但你需要安装 [unplugin-element-plus](https://github.com/element-plus/unplugin-element-plus) 来导入样式。

```html
<template>
  <el-button>我是 ElButton</el-button>
</template>
<script>
  import { ElButton } from 'element-plus'
  export default {
    components: { ElButton },
  }
</script>
```

```js
import { defineConfig } from 'vite'
import ElementPlus from 'unplugin-element-plus/vite'

export default defineConfig({
  // ...
  plugins: [ElementPlus()],
})
```

## 全局配置

在引入 ElementPlus 时，可以传入一个包含 `size` 和 `zIndex` 属性的全局配置对象。 `size` 用于设置表单组件的默认尺寸，`zIndex` 用于设置弹出组件的层级，`zIndex` 的默认值为 `2000`。

完整引入：

```js
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import App from './App.vue'

const app = createApp(App)
app.use(ElementPlus, { size: 'small', zIndex: 3000 })
```

按需引入:

```vue
<template>
  <el-config-provider :size="size" :z-index="zIndex">
    <app />
  </el-config-provider>
</template>

<script>
import { defineComponent } from 'vue'
import { ElConfigProvider } from 'element-plus'

export default defineComponent({
  components: {
    ElConfigProvider,
  },
  setup() {
    return {
      zIndex: 3000,
      size: 'small',
    }
  },
})
</script>
```

# 
