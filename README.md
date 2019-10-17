# gitlearn

### 1.创建
- 创建git版本库：  
`$ git init`

- 查看git状态：  
`git status`

- 添加文件到缓冲区：  
`git add <file>`  
`git add -A  提交所有变化`  
`git add -u  提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)`  
`git add .  提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件`  

- 移除缓冲区：  
`git reset -- <file> 把某个文件重置为未添加的状态，用这个命令可以保证某个文件不被添加到缓冲区`  

- 删除文件：  
`git rm <file>`

- 提交缓冲区内容，-m <msg> 是添加提交日志：  
`git commit -m "<msg>"`

- 查看提交日志：  
```
//查看多行日志
git log
//查看简易日志
git log --pretty=oneline
```

### 2.版本回退
- 回退上一个版本：  
`$ git reset --hard HEAD^`

- 跳转到某一个版本：  
`$ git reset --hard 1094a`  
其中1094af就是在log中看到的版本号中的某几位，不用写全也可以

- 查看输入的命令记录：  
`git reflog`

- 总结
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。  
穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。  
要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

### 3.撤销修改
- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- <file>`

- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

### 4.提交到github
- 查看远程库：  
`$ git remote`

- 添加远程库:
```
$ git remote add <remotename> git@github.com:Jungle2329/getlearn.git
其中<remotename>一般默认是origin
github的服务器 git@github.com
github的名字和项目名 Jungle2329/getlearn.git
```
- 这里有个很重要的点，远程库不一定是github的，局域网的地址，或者本地不同文件夹下都可以作为远程库  
可以选择remotename用来提交到不同的远程库
```
$ git remote add <remotename> <url>
url：
github服务器 	 git@github.com:Jungle2329/gitlearn.git
本地				 D:/test/gitlearn
局域网			 <ip>D:/test/gitlearn
```

- 从远程库克隆到本地：  
`$ git clone git@github.com:Jungle2329/getlearn.git`

- 提交到远程库：  
`$ git push <name>`

- 从远程库拉取：  
`$ git pull`


### 5.分支
- 查看分支：  
`git branch`

- 创建分支name：  
`git branch <name>`

- 切换分支name：  
`git checkout <name>`

- 创建并切换分支name：  
`git checkout -b <name>`

- 在本地创建dev并切换到远程origin分支dev：  
`$ git checkout -b dev origin/dev`

这时就可以在分支工作了，工作完再合并到master上

- 合并name到当前分支：  
`git merge <name>`

- 删除分支name：  
`git branch -d <name>`

### 6.解决冲突
用带参数的git log也可以看到分支的合并情况：
`git log --graph --pretty=oneline --abbrev-commit`  
出现冲突的时候使用`git status`可以查看哪个文件出现了冲突，找到该文件，冲突的地方会以`>>>>>`,`=====`,`<<<<<`标记冲突的区域

	<<<<<<< HEAD
	Creating a new branch is quick & simple.
	=======
	Creating a new branch is quick AND simple.
	>>>>>>> feature1


### 7.分支管理策略
使用`git merge dev`的时候默认使用`Fast forword`模式，这种模式下，删除分支后，会丢掉分支信息  
如果想要强制禁用`Fast forword`可以使用如下方法：  
```
$ git merge --no-ff -m "提交日志" dev
本次合并会创建一个commit所以需要 -m "日志"
```

### 8.bug修复使用stash功能保存当前工作进度
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

### 9.使用-D来强制删除未合并的分支
当正在开发的分支不用的时候，不能合并进主分支，又想要删除当前分支的数据：  
```
使用		git branch -d feature 是删不掉的
要使用	git branch -D feature 强制删除未合并的分支
```

### 10.多人协作
- 查看远程库的信息：  
`$ git remote`

- 查看远程库的具体信息：  
`$ git remote -v`

`多端的远程库名字必须是相同的，不然无法使用`

-删除远程库
`$ git remote remove [远程库]`

- 推送分支：  
`$ git push origin master`

- 推送其他分支：  
`$ git push origin dev`

`master`分支是主分支，因此要时刻与远程同步；

`dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

`bug`分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

`feature`分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

- 多人开发的流程：  
 1. 查看远程库信息，使用git remote -v；
 - 本地新建的分支如果不推送到远程，对其他人就是不可见的；
 - 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
 - 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
 - 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
 - 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

### 11.标签

- 给当前`HEAD`打标签：  
`$ git tag v1.0`
- 给某个版本打标签：  
`$ git tag v1.1 65f5d1f`  
- 打带有信息的标签：  
`$ git tag -a v1.2 -m "msg"`
- 查看所有标签：  
`$ git tag`
- 展示标签：  
`$ git show v1.1`
- 删除标签：  
`$ git tag -d v1.0`
- 推送某个标签到远程：  
`$ git push origin v1.0`
- 推送所有尚未推送的标签到远程：  
`$ git push origin --tags`
- 如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：  
`$ git tag -d v1.0`  
然后，从远程删除。删除命令也是push，但是格式如下：  
`$ git push origin :refs/tags/v1.0`

### 12.忽略
- 直接添加忽略的方案到.ignore  
- 强行提交已经被忽略的文件：  
`$ git add -f <file>`
查看文件忽略状态：  
`$ git check-ignore -v <file>`
- Git忽略规则：  
```
在git中如果想忽略掉某个文件，不让这个文件提交到版本库中，可以使用修改根目录中 .gitignore 文件的方法（如果没有这个文件，则需自己手工建立此文件）。这个文件每一行保存了一个匹配的规则例如：

 # 此为注释 – 将被 Git 忽略
*.sample 　　 # 忽略所有 .sample 结尾的文件
!lib.sample 　　 # 但 lib.sample 除外
/TODO 　　 # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/ 　　 # 忽略 build/ 目录下的所有文件
doc/*.txt 　　# 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```
- .gitignore规则不生效的解决办法：  
```
把某些目录或文件加入忽略规则，按照上述方法定义后发现并未生效，原因是.gitignore只能忽略那些原来没有被追踪的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。那么解决方法就是先把本地缓存删除（改变成未被追踪状态），然后再提交：

git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```


### 13.git修改日志的方法
有时候，日志已经提交了，但是发现还有要修改的地方，需要以以下的方法来修改，主要有4中情况

1. 需要修改最后一次的提交，而且还没有push  
`git commit --amend`  
之后进入vi编辑器，直接修改就好，插入为i，保存并关闭为wq

- 需要修改最后一次的提交，但是push了  
`git commit --amend`  
`git push origin master --force`  
和情况1的做法一样。使用push推送到远程服务器是需要加上--force，让服务器更新历史记录。  
**需要注意的是：把修改后的日志强制push到Git服务器，如果别人本地的副本有修改，很有可能会导致他们同步不了，所以最好和他们核对下。**

- 需要修改某次的提交，而且还没有push  
假设commit是倒数第3次提交，这个可以使用git rebase修改编辑状态  
`git rebase -i HEAD~3`  
它会打开一个编辑器，它会把最后前3次的提交显示出来，类似于：  
`pick 94fc8fe 添加内容a`  
`pick 04f0d18 添加内容c`  
`pick b1b451d 添加内容d`  
这时需要把pick修改为edit，类似于：  
`pick 94fc8fe 添加内容a`  
`edit 04f0d18 添加内容c`  
`pick b1b451d 添加内容d`  
接着使用：  
`git commit --amend`  
完成编辑后使用提交修改  
`git rebase --continue`

- 需要某次的提交，但是push了  
修改方法基本和情况3相同  
`git rebase -i HEAD~X`  
`git commit --amend`  
`git rebase --continue`  
X表示倒数第几次提交。  
完成编辑日志后，执行push：  
`git push origin master --force`  
**注意：这个情况二相似，把修改后的日志强制push到Git服务器，如果别人本地的副本有修改，很有可能会导致他们同步不了，所以最好和他们核对下。**



### git常用功能补充
`git show <filename>` 可以查看该文件的修改信息
`git log --pretty=oneline <filename>` 可以查看该文件的提交日志


