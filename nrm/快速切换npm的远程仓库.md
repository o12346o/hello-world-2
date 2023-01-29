# nrm

用来快速切换 npm 的远程仓库。

## 查看可用的远程仓库

```bash
nrm l
```

显示出可用的远程仓库

```
  npm ---------- https://registry.npmjs.org/
  yarn --------- https://registry.yarnpkg.com/
  tencent ------ https://mirrors.cloud.tencent.com/npm/
  cnpm --------- https://r.cnpmjs.org/
  taobao ------- https://registry.npmmirror.com/
  npmMirror ---- https://skimdb.npmjs.com/registry/
```

## 使用指定的远程仓库

```bash
nrm use 仓库名
```

## 查看 npm 的配置

```bash
npm config list
```