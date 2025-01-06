# 恢复已删除的分支

操作流程：

1. `git reflog show`查看commitid

2. `git checkout -b 新分支名称 要恢复的commitid值`根据commitid值创建新分支，即可恢复已删除的分支 
