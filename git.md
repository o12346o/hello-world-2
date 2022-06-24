# git 使用帮助说明

## 1、git 本地仓库

    git init //初始化，创建本地仓库
    git add 文件名 //添加到暂存区
    git add . //所有文件添加到暂存区
    git commit -m '注释'  //提交到本地仓库，添加注释，也可以进入vi 添加注释
    git status //查看git此时的提交状态
    git log //查看提交记录
    git reset --hard HEAD^ //回退上一个版本
    git reflog //查看操作记录
    git reset --hard 版本号 //回退到指定版本

## 2、git 远程仓库

    //链接远程仓库
    
    git config --global user.name "用户名"
    git config --global user.name "用户邮箱"
    git remote add origin 仓库地址 //链接远程仓库
    
    git remote rm origin //删除链接远程仓库
    git remote set-url origin <url>  // 修改远程仓库地址
    
    //将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。
    
    git push -u origin master //-u指明默认仓库，然后推送到远程仓库
    git push origin master //推送到远程仓库
    
    git push //推送到默认仓库

## 3、git 两人协作-非冲突

    git clone 远程仓库地址 //克隆远程仓库
    git pull origin master //从远程仓库拉取更新，和本地仓库合并，保留新的内容（本地或远程）
    
    1）拉取远程仓库更新 
    2）自己的工作
    3）自己的工作先提交到本地仓库，再拉取远程仓库更新。
    4）提交自己的工作到远程仓库。

## 4、git 两人协作-冲突

    两个人同时修改了一个文件，产生冲突，需要通过对比，手动合并。
    
    vscode可视化工具

## 5、git 分支

1.0版本发布，通过分支，开发2.0版本、或修复bug。  
在分支上修改，不影响主分支。

    git branch -a //查看所有分支
    git branch -M main //-M 重命名主分支为 main
    master //默认本地主分支master
    git checkout -b 分支名 //创建新分支
    git checkout 分支名 //切换分支
    git merge 分支名 //合并分支
    
    git push origin 分支名 //将分支推送到远程仓库
    git push origin master:分支名 //推送master到远程的分支
    git push origin :分支名 //删除远程分支
    git branch -d 分支名 //删除本地分支

## 6、git 初始化流程

```
echo "# hello-world-2" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/o12346o/hello-world-2.git
git push -u origin main
```

## 7、git 日常工作

```
git add .
git commit -m '注释'
git push
```

<mark>注意事项：</mark> git项目目录中最好不要使用中文。

VScode使用<kbd>ctrl</kbd>+<kbd>shift</kbd>+<kbd>v</kbd>预览 markdown 文件

VScode使用<kbd>ctrl</kbd>+<kbd>k</kbd>放掉,然后<kbd>v</kbd>实时预览markdown文件