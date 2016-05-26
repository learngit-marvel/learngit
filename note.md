# 分支管理
## 创建与合并分支
- 查看分支：`git branch`
- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>`
- 创建+切换分支：`git checkout -b <name>`
- 合并某分支到当前分支：`git merge <name>`
- 删除分支：`git branch -d <name>`
<br/>

## 解决冲突
查看分支合并图：`git log --graph`
<br/>

## 分支管理策略
合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。<br/>
master分支用于发布新版本，dev分支用于开发。开发者向dev合并各自的分支，发布新版本时把dev分支合并到master上。<br/>

## Bug分支
1. 使用`git stash`命令保存现场（假设在dev分支上）
2. 切换到出现Bug的分支（假设为master分支），创建Bug分支修复bug
3. 切换回master分支，合并Bug分支后将其删除
4. 恢复现场：
   - 查看记录：`git stash list`
   - 恢复并删除记录：`git stash pop`
   - 恢复记录：`git stash apply`
   - 恢复指定记录：`git stash apply <stash@{id}>`
   - 删除记录：`git stash drop`
<br/>

## 多人协作
查看远程库（详细）信息：`git remote [-v]`
<br/>

### 推送分支
`git push origin master`  `git push origin dev`
- master分支是主分支，因此要时刻与远程同步；
- dev分支是开发分支，团队所有成员都需要在上面工作，也需要与远程同步；
- bug分支只用于在本地修复bug，不必要推到远程;
- feature分支是否推到远程，取决于在上面是否有合作开发。
<br/>

### 抓取分支
`git push origin dev`
- 默认情况下，从远程库clone时只能看到master分支。
- 要在dev分支上开发，必须创建远程origin的dev分支到本地：`git checkout -b dev origin/dev`。
<br/>

### 工作模式
1. 首先，可以试图用`git push origin branch-name`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！
<br/>*如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。*
<br/>

# 标签管理
- 新建标签：`git tag <tagname> [commit id]`
- 查看标签：`git show <tagname>`
- 查看所有标签：`git tag`
- 推送标签：`git push origin <tagname>`
- 推送全部标签：`git push origin --tags`
- 删除本地标签：`git tag -d <tagname>`
- 删除远程标签：`git push origin :refs/tags/<tagname>`
<br/>*创建的标签只存储在本地，不会自动推送到远程*<br/>
`git tag -a <tagname> -m "blablabla..."`*可以指定标签信息*<br/>
`git tag -s <tagname> -m "blablabla..."`*可以用PGP签名标签*<br/>
