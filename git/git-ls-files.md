# git怎么查看哪些文件是在版本控制下的呢?

## 1、git status

`git status` 命令只能查看缓冲区内哪些文件发生了变化。若其中没有文件发生变化，就无法查看缓冲区内有哪些文件。

```
$ git status
On branch main
Your branch is ahead of 'origin/main' by 15 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git-rm.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git-ls-files.md
        test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

## 2、git ls-files

`git ls-files` 命令可以查看缓存区内有哪些文件。

```
$ git ls-files
.gitignore
MarkText.md
Node/Node01.md
Node/Node02.md
Node/Node03.md
Node/Node04.md
README.md
git-rm.md
git.md
gitignore.md
markdown.md
```

## 3、git文件分类

git 将所有文件分为三类：已追踪的、被忽略的、未被追踪的。

### 1、已追踪的（Tracked）

已经追踪的文件是指已经在缓存区中的文件，或者是已经在版本库中的文件。

只需将文件添加到缓存区，文件就会被追踪（）。

```
git add test.txt
```

### 2、被忽略的（Ignored）

被忽略的文件必须在版本库中明确指明不可见或被忽略，即使被忽略的文件可能在工作区出现。

通过编写 .gitignore 文件 指明被忽略的文件。.gitignore 文件 必须提前存在于版本库中才能起作用。

```gitignore
# 忽略 .html 格式的文件
*.html
```

### 3、未被追踪的（Untracked）

未被追踪的文件是只那些即没有添加到缓存区、也没有被忽略的文件。

例如，新建了一个文件 hello.c ，既没有被忽略，也没有`git add hello.c` ，hello.c 文件即为未被追踪的文件。


