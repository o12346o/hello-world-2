# 忽略文件.gitignore的使用

1. 首先，在你的工作区新建一个名称为.gitignore的文件。
2. 然后，把要忽略的文件名或目录名填进去，Git就会自动忽略这些文件或目录名。

## 1、.gitignore 文件中的语法

忽略指定的文件或目录

```gitignore
# 忽略指定的文件
hello.c

# 忽略指定的文件夹
bin/
test/bin/
```

通配符规则

- `*` 表示零个或多个字符 

- `?` 表示一个字符 

- `!` 表示不忽略

- `**` 表示多级路径

```gitignore
# 忽略.class的所有文件
.class

# 不忽略 hello.class文件
！hello.class

# 忽略名称中末尾为ignore的文件夹
*ignore/

# 忽略名称中间包含ignore的文件夹
*ignore*/
```

## 2、初始化 .gitignore 规则

在git初始化准备工作完成后，

```
echo "# hello-world-2" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/o12346o/hello-world-2.git
git push -u origin main
```

紧接着添加 .gitignore 规则。（.gitignore 文件可手动创建，也可以使用bash命令创建）

```
git add .gitignore
git commit -m '添加 .gitignore'
git push
```

## 3、强制添加已经被忽略的文件到git中

强制添加 git.html 文件

```
git add git.html -f
```

## 4、忽略已经添加到git中的文件

```
git rm git.html --cached
```

## 5、更新 .gitignore 文件

1、清除git本地缓存

```
git rm -r --cached .
```

2、添加 .gitignore 文件

```
git add .gitignore
```

3、提交 .gitignore 文件

```
git commit -m '更新 .gitignore'
```
