# Vue中的CSS深度选择器

在单组件中使用 elementUI 的组件库时，需要对el-xxx进行样式修改。

可以通过CSS深度选择器进行修改（Vue 中独有）。

```html
<style scoped>
:deep(.el-xxx){
    background: #f00;
}
</style>
```

也可以用 `/deep/样式名` 、`::deep 样式名` 、`>>>样式名` 、`v-deep 样式名` 。（这几个不推荐）


