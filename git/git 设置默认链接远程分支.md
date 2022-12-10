推送时设置默认仓库分支

```bash
git push -u origin master    # -u 指明默认仓库，然后推送到远程仓库 master 分支
```

单纯修改默认远程仓库分支

```bash
git branch -u origin/test    # 修改默认远程仓库 test 分支

# 或者是以下这个，也可以修改默认远程分支
git branch --set-upstream-to=origin/test 
```