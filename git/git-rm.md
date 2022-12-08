# git rm 命令使用

git 本地数据管理，可以分为三个区：

- 工作区（Working Directory）：是可以直接编辑的地方。
- 暂存区（Stage/Index）：数据暂时存放的区域。
- 版本库（commit History）：存放已经提交的数据。

## 1.1 rm 命令

**1、作用：** 删除工作区的文件。

**2、作用对象：** 在工作区中的文件。 

执行删除命令：

```
$ rm test.txt
```

查看状态：

```
$ git status
On branch main

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

rm 命令只是删除了工作区的文件，并没有将这次删除记录到暂存区，也没有删除版本库的文件。

**3、后续操作**

添加到暂存区中：

```
 git add test.txt
```

提交到版本库中：

```
$ git commit -m 'rm 测试'
[main c672d0d] rm 测试
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 test.txt
```

## 1.2 git rm 命令

**1、作用：** 删除工作区文件，并将这次删除记录到暂存区。

**2、作用对象：** 已经在版本库中，且没有修改过的文件。

执行删除命令：

```
$ git rm test.txt
rm test.txt
```

git rm 命令删除了工作区的未修改的文件，还将这次删除记录到暂存区，但是没有删除版本库的文件。

**3、后续操作**

提交到版本库中：

```
$ git commit -m 'git rm 测试'
[main 84e2872] git rm 测试
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 test.txt
```

## 1.3 git rm -f 命令

**1、作用：** 删除工作区文件和暂存区文件，并将这次删除记录到暂存区。

**2、作用对象：** 已经在版本库中，且修改过的文件。

执行删除命令：

```
$ git rm -f test.txt
rm test.txt
```

git rm -f 命令强制删除了工作区的已经修改的文件，还将这次删除记录到暂存区，但是没有删除版本库的文件。

**3、后续操作**

提交到版本库中：

```
$ git commit -m 'git rm -f 测试'
[main 5771e3c] git rm -f 测试
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 test.txt
```

## 1.4 git rm --cached 命令

**1、作用：** 删除暂存区文件，保留工作区文件，并将这次删除记录到暂存区。

**2、作用对象：** 已经在版本库中，且修改过的文件。

```
$ git rm --cached test.txt
rm test.txt
```

git rm --cached 命令保留了工作区文件，删除了暂存区文件，并将这次删除记录到暂存区，，但是没有删除版本库的文件。

**3、后续操作**

提交到版本库中：

```
$ git commit -m 'git rm --cached 测试'
[main 4fefd61] git rm --cached 测试
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 test.txt
```
