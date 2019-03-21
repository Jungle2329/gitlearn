# gitlearn

### 1.创建
查看git状态：
`git status`

添加文件到缓冲区：
`git add <file>`

提交缓冲区内容，-m <msg> 是添加提交日志：
`git commit -m "<msg>"`

查看提交日志：

```
$ git status
On branch dev  
nothing to commit, working tree clean  
```

### 1.分支
查看分支：
```git branch```

创建分支name：
```git branch <name>```

切换分支name
```git checkout <name>```

创建并切换分支name：
```git checkout -b <name>```

合并name到当前分支：
```git merge <name>```

删除分支name：
```git branch -d <name>```
