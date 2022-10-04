# 提升开发体验

## sourceMap

### 为什么

开发环境下，代码运行出错，提示位置为编译后代码位置，不容易查找错误位置。

需要更加准确的错误提示，以便于修改错误。

### 是什么

SourceMap（源代码映射）是一个用来生成源代码与编译后代码一一映射的文件的方案。

它会生成一个 xxx.map 文件，里面包含源代码和编译后代码每一行、每一列的映射关系。当构建后的代码出现错误时，会通过 xxx.map 文件，从构建后代码出错的位置映射到源代码出错的位置，从而让浏览器提示源代码出错位置。

### 怎么用

- **开发模式** ：`cheap-module-source-map` 
  
  - 优点：打包编译速度快，只包含行映射
  
  - 缺点：没有列映射

```js
module.exports = {
    // 其他代码省略
    mode: "development",
    devtool: "cheap-module-source-map"
}
```

- **生产模式** ：`source-map`
  
  - 优点：包含行/列映射
  
  - 缺点：打包编译速度更慢

```js
module.exports = {
    // 其他代码省略
    mode: "production",
    devtool: "source-map"
}
```
