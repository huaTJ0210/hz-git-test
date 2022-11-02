### git init

> 初始化仓库,生成.git 目录

### git add xx / git add .

> 将修改添加到暂存区

### git commit -m'change message'

> 将暂存区的内容纳入到版本控制中,并标注修改的简介

### git branch your-branch-name

> 创建分支

### git checkout branch-name

> 切换到指定的分支

### git checkout -b branch-name

> 创建并切换到指定的分支

### git branch -d branche-name

> 删除指定的分支

### git merge xxx

> 将当前分支与 xx 进行合并

### git rebase xx

> 与 xx 进行合并，能得到线性的提交记录

### HEAD

> HEAD 是一个指针，指向的是当前工作分支最近一次提交
> 通过 git checkout xx 即能改变当前 HEAD 的指向
### 相对引用
> 避免使用哈希值来指定移动提交记录，可以使用相对引用（~）来简化
> ~num ： num代表向上移动的提交记录步数

### 强行修改分支
> git branch -f main HEAD~3
> 上面的命令会将 main 分支强制指向 HEAD 的第 3 级父提交。