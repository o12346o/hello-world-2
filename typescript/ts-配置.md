# ts配置

tsconfig.json 配置文件中

```json
{
  "include":[],
  "compilerOptions": {
    // 指明要编译到ECMAScript哪个版本
    "target": "ES6",
    // 指明是否要移出注释
    // "removeComments": false,
    // 指定使用模块
    // "module": "ES6",
    // 是否允许编译js
    // "allowJs": false,
    // 输出路径
    "outDir": "./js",
    // 输出文件，将所有ts编译到一个文件中
    // "outFile": "./bundle.js",
    // ts文件中有错误时是否编译
    "noEmitOnError": true
  }
}
```

当运行 `tsc` 命令时，会使用 `tsconfig.json`中的配置。