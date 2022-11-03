[learn git](https://learngitbranching.js.org/?locale=zh_CN)

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

### git rebase

#### git rebase  branchName
> 将当前分支的提交移动到branchName的HEAD之后

#### git rebase current branchName

> 将 branchName（包含在此分支上的多次提交）合并到 current的HEAD 后
> 如果在同一分支路径上，可以让 branchName 快速前进（和当前分支的HEAD保持一致）

#### git rebae的优缺点
> 优点：Rebase 使你的提交树变得很干净, 所有的提交都在一条线上
> 缺点：Rebase 修改了提交树的历史

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

#### git revert xx

> 为了撤销更改并分享给别人，我们需要使用 git revert。
> git revert 会产生一个新的提交记录，revert 后可以将更改推送到远程仓库

### 整理提交记录

#### git cherry-pick <提交号>

> cherry-pick 可以将提交树上任何地方的提交记录取过来追加到 HEAD 上（只要不是 HEAD 上游的提交就没问题
> 场景: 在某个开发分支上有多个提交记录，需求是只合并最后的那次提交
> 则可以先切换到 master 分支，然后使用 git cherry-pick <lastCommitHash> 完成

#### 交互式的 git rebase

> git rebase -i xx ： 获取提交记录（可以移除或者改变提交记录）

### git tag

> tag 永久地将某个特定的提交命名为里程碑，然后就可以像分支一样引用了。
> git tag tagName <指定的提交记录默认是 HEAD>

### 远程分支命名规范

> <remote name> / <branch name>

### git fetch

> 1、从远程仓库下载本地仓库中缺失的提交记录
> 2、在本地更新远程分支指针(如 origin/main)

#### git fetch origin <place>
> 只下载了远程仓库中 place 分支中的最新提交记录，并更新了 origin/foo

#### git fetch origin :bar
> 如果 fetch 空 到本地，会在本地创建一个新分支。

### git pull

> 抓取远程仓库的更新，并与本地分支进行合并
> 对于 git pull，其实就是（git fetch 及 git merge 的缩写）
#### git pull --rebase
> 拉取远端更新时采用rebase的方式进行

#### git pull origin main
> 从远端仓库拉取main的提交记录，并在本地更新origin/main(默认绑定)，然后再与当前HEAD进行merge操作

#### git pull origin main:foo
> 先在本地创建了一个叫 foo 的分支，从远程仓库中的 main 分支中下载提交记录，并合并到 foo，然后再 merge 到我们的当前检出的分支 xxx 上

### git push

> 推送本地分支到远程仓库

#### git push <remote> <place>
> git push origin main: 
> 上述命令的执行步骤：1、切到本地仓库中的place分支，获取所有的提交，2、到远程仓库“origin”中找到place分支，将远程仓库中没有的提交记录都添加上去
#### git push origin <source>:<destination>
> 提交本地分支内容： soure-本地分支，destination-远端分支

#### git push origin :foo
> push传递空值source，成功删除远程仓库的foo分支



#### 提交代码场景（git push 被拒绝）
> 基于远程分支开发的功能本地有提交，远端仓库也有提交，此时直接使用 git push 是不被允许的
##### 使用git rebase解决

> 需要先获取远程更新到本地（git fetch），然后与本地进行合并（git rebase origin/xxx）,最终再进行提交（git push）
> 使用git rebase能保证远端仓库提交的线性

##### 使用git merge解决
> 需要先获取远程更新到本地（git fetch），然后与本地进行合并（git merge origin/xxx）,最终再进行提交（git push）；这样做远端会有本地合并的操作留痕
> 使用git merge会导致远端仓库提交记录不是线性的 

### pull request流程

#### 场景：忘记了创建分支，直接push会被拒绝
> 新建一个分支feature, 推送到远程服务器. 然后reset你的main分支和远程服务器保持一致, 否则下次你pull并且他人的提交和你冲突的时候就会有问题.

### 远程跟踪

> 本地仓库与远端进行关联（remote tracking）
> 关联的时机是在git clone之后（git clone操作之后的输出：local branch "main" set to track remote branch "origin/main"）

### 设置远程追踪分支
#### 方法1： 创建分支并跟踪远程分支
> git checkout -b localBranch origin/main
#### 方法2：使用git branch -u
> git branch -u origin/main  branchName
> 上述命令会使得branchName追踪 origin/main

