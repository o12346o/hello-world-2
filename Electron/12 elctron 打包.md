# elctron 打包

## 使用 electron-builder 打包

安装electron-builder

```shell
npm install electron-builder -D
```

项目下配置`.npmrc`文件，文件中指明electron-builder的镜像源

```
electron_builder_binaries_mirror=https://registry.npmmirror.com/-/binary/electron-builder-binaries/
```

在`package.json`中，添加脚本命令

```json
{
  "scripts":{
      "pack": "electron-builder --dir",
      "build": "electron-builder"
    }
}
```

构建包含含应用程序的文件夹（免安装软件）

```shell
npm run pack
```

构建应用程序（含安装软件）

```shell
npm run build
```

**注意**：若运行 npm run pack 或 npm run build 报错cannot execute cause=exit status 时，应以管理员身份运行shell。

## 自定义打包配置

在`package.json`文件中，添加配置

```json
"build": {
  "productName": "demo", // 应用名称
  "appId": "com.my.demo", // 应用唯一标识符
  "win": { // windows 平台
    "icon": "path/img/icon.ico", // 应用的图标
    "target": [ // 构建目标
      {
        "target": "nsis", // 适应 nsis 创建安装程序
        "arch": ["x64"] // 构建 x64 架构的版本
      }
    ]  
  },
  "nsis": { // nsis安装程序的相关配置
    "oneClick": false, // 是否一键安装
    "perMachine": true, // 将应用安装到所有用户的全局位置
    "allowToChangeInstallationDirectory": "true" // 允许用户更改安装位置
  }
}
```
