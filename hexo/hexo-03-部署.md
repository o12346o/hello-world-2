# 部署

## 1、安装 hexo-deployer-git。

```bash
$ npm install hexo-deployer-git --save
```

## 2、修改配置。

在 _config.yml 中修改参数：

```yml
deploy:
  type: git
  repo: <repository url> 
  branch: [branch]
  message: [message]
```

| 参数        | 描述              | 默认                                                                      |
| --------- | --------------- | ----------------------------------------------------------------------- |
| `repo`    | 库（Repository）地址 |                                                                         |
| `branch`  | 分支名称            | `gh-pages` (GitHub)<br>`coding-pages` (Coding.net)<br>`master` (others) |
| `message` | 自定义提交信息         | `Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}`)                       |

可以配置多个远程仓库：

```yml
deploy:
  - type: git
    repo: <repository url-1> 
    branch: [branch]
    message: [message]
  - type: git
    repo: <repository url-2> 
    branch: [branch]
    message: [message]
```

## 3、生成站点文件并推送至远程库。执行 `hexo clean` && `hexo deploy`。

## 4、远程库更新后，需要对 Pages 服务进行更新。