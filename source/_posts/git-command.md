---
title: 工作中常遇到的场景git命令备忘
date: 2019-12-18 19:13:32
tags:
- git
---
## 场景1
开发中需要暂存当前分支的内容，切换到另外一个分支进行开发。
离开当前分支保存当前修改的内容：
```javascript
    git add .
    git commit -m "description"
```

回到当前分支撤销上次commit并保留修改的文本在工作区：
```javascript
    git reset --soft HEAD^
```
    
## 场景2
同时维护的两个版本出现了同一个bug，在一个分支修改后，另外一个分支也要修复当前bug，可以使用如下命令将修改的内容拷贝过来：
```javascript
    git cherry-pick commit-sha1
```

## 场景3
新拉的功能分支开发完毕后需要合并到主分支，如果直接合过去就会产生很多commit，git提交记录会分叉，这时可以使用rebase命令让我们的记录看起来更清爽：
```javascript
    git rebase <branch>
```
接下来按照提示操作即可
