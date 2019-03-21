# gitlearn

### 1.创建
查看git状态：  
`git status`

添加文件到缓冲区：  
`git add <file>`

删除文件：  
`git rm <file>`

提交缓冲区内容，-m <msg> 是添加提交日志：  
`git commit -m "<msg>"`


查看提交日志：  
```
//查看多行日志
git log
//查看简易日志
git log --pretty=oneline
```

### 2.提交到github
查看远程库：  
`git remote`

添加远程库:
```
git remote add <remotename> git@github.com:Jungle2329/getlearn.git
其中<remotename>一般默认是origin
github的服务器 git@github.com
github的名字和项目名 Jungle2329/getlearn.git
```
 
从远程库克隆到本地库：  
`git clone git@github.com:Jungle2329/getlearn.git`

提交到远程库：  
`git push <name>`

### 3.分支
查看分支：  
`git branch`

创建分支name：  
`git branch <name>`

切换分支name：  
`git checkout <name>`

创建并切换分支name：  
`git checkout -b <name>`

这时就可以在分支工作了，工作完再合并到master上

合并name到当前分支：  
`git merge <name>`

删除分支name：  
`git branch -d <name>`

### 4.解决冲突
用带参数的git log也可以看到分支的合并情况：
`git log --graph --pretty=oneline --abbrev-commit`

### 5.分支管理策略
使用`git merge dev`的时候默认使用`Fast forword`模式，这种模式下，删除分支后，会丢掉分支信息  
如果想要强制禁用`Fast forword`可以使用如下方法：  
```
$ git merge --no-ff -m "提交日志" dev
本次合并会创建一个commit所以需要 -m "日志"
```

### 6.bug修复使用stash功能保存当前工作进度
当开发一半的时候，有bug需要修改，可以把当前进度使用stash功能保存  
`$ git stash`  
保存后当前分支就是完全clean的状态，这时可以查看保存的信息
```
$ git stash list
stash@{0}: WIP on dev: f52c633 add merge
```
保存后可以再任意修改bug或者使用分支修改bug后提交，提交后使用

现在需要还原保存的stash，有两种方法：  
一是用`git stash apply`恢复，但是恢复后，`stash`内容并不删除，你需要用`git stash drop`来删除；  
二是用`git stash pop`同时恢复并且删除`stash`

你可以多次`stash`，恢复的时候，先用`git stash list`查看，然后恢复指定的`stash`，用命令：  
`$ git stash apply stash@{0}`