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

### 提交到github
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

傻逼
超傻逼