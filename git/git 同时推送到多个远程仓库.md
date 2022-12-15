# git 同时推送到多个远程仓库

## 方式一：通过 git 命令添加

```git
# 链接 github（第一个远程仓库）
git remote add origin github地址 

# 链接 gitee（第二个远程仓库）
git remote set-url --add origin gitee地址
```

## 方式二：通过修改 git 的config文件添加远程仓库

```
[core]
    repositoryformatversion = 0
    filemode = false
    bare = false
    logallrefupdates = true
    symlinks = false
    ignorecase = true
[remote "origin"]
    url = git@github.com:o12346o/hello-world-2.git
    fetch = +refs/heads/*:refs/remotes/origin/*
  + url = git@gitee.com:o12346o/hello-world-2.git
[branch "main"]
    remote = origin
    merge = refs/heads/main
```

`git push origin` 时，即可同时推送到github 和 gitee。

## 查看远程仓库情况

```bash
git remote -v
```

## 链接两个仓库并分别起名

```git
git remote add name01 git@github.com:o12346o/hello.git
git remote add name02 git@github.com:o12346o/hello.git
```

`git push name01` 推送到 github，`git push name02` 推送到 gitee。