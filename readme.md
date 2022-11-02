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

### git rebase current  branchName

> 将branchName（包含在此分支上的多次提交）合并到current后
> 如果在同一分支路径上，可以让branchName快速前进

### HEAD

> HEAD 是一个指针，指向的是当前工作分支最近一次提交
> 通过 git checkout xx 即能改变当前 HEAD 的指向

### 相对引用

> 避免使用哈希值来指定移动提交记录，可以使用相对引用（~）来简化
> ~num ： num 代表向上移动的提交记录步数

### 强行修改分支

> git branch -f main HEAD~3
> 上面的命令会将 main 分支强制指向 HEAD 的第 3 级父提交。

### 撤销变更

#### git reset xx

> git reset 通过把分支记录回退几个提交记录来实现撤销改动。你可以将这想象成“改写历史”。git reset 向上移动分支，原来指向的提交记录就跟从来没有提交过一样。

#### git revert

> 为了撤销更改并分享给别人，我们需要使用 git revert。
> git revert 会产生一个新的提交记录，revert 后可以将更改推送到远程仓库

### 整理提交记录

#### git cherry-pick <提交号>
> cherry-pick 可以将提交树上任何地方的提交记录取过来追加到 HEAD 上（只要不是 HEAD 上游的提交就没问题
> 场景: 在某个开发分支上有多个提交记录，需求是只合并最后的那次提交
> 则可以先切换到master分支，然后使用git cherry-pick <lastCommitHash> 完成

#### 交互式的git rebase
> git rebase -i  xx  ： 获取提交记录（可以移除或者改变提交记录）

### git tag
> tag永久地将某个特定的提交命名为里程碑，然后就可以像分支一样引用了。
> git tag tagName <指定的提交记录默认是HEAD>