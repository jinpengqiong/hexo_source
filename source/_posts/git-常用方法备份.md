---
title: git 常用方法备份
date: 2020-06-12 15:53:49
tags:
---
- branch
```bash
1.列出分支，-a参数是列出所有分支，包括远程分支
git branch [-a]

2.创建一个本地分支
git branch branchname

3.创建一个分支，并切换到该分支
git checkout -b branchname

4.删除一个本地分支
git branch -d branchname

5.删除一个远程分支
git push origin --delete branchname

6.删除一个远程分支，通过push一个空的分支来覆盖原来的分支，以达到删除远程分支的目的
git push origin :branchname
```

- tag
```bash
1.列出分支，-a参数是列出所有分支，包括远程分支
git branch [-a]

2.创建一个本地分支
git branch branchname

3.创建一个分支，并切换到该分支
git checkout -b branchname

4.删除一个本地分支
git branch -d branchname

5.删除一个远程分支
git push origin --delete branchname

6.删除一个远程分支，通过push一个空的分支来覆盖原来的分支，以达到删除远程分支的目的
git push origin :branchname
```