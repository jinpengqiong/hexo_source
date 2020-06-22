---
title: git rebase 和 merge区别
date: 2020-06-22 10:53:46
tags:
---
git rebase一般解释为变基，也有解释为衍合。

git merge 和 git rebase 都可以整合两个分支的内容，最终结果没有任何区别，但是变基使得提交历史更加整洁。
#### 提交点顺序
- git merge后，提交点的顺序都和提交的时间顺序相同，即 master 的提交在 dev 之后。
- git rebase后，顺序变成被rebase的分支（master）所有提交都在前面，进行rebase的分支（dev）提交都在被rebase的分支之后，在同一分支上的提交点仍按时间顺序排列。
#### 分支变化
- dev 在 rebase master 后，由原来的两个分岔的分支，变成重叠的分支，看起来 dev 是从最新的 master 上拉出的分支。
#### 什么时候使用 rebase / merge
假设场景：从 dev 拉出分支 feature-a。那么当 dev 要合并 feature-a 的内容时，使用 git merge feature-a；反过来当 feature-a 要更新 dev 的内容时，使用 git rebase dev。
使用时主要看两个分支的"主副"关系。
注意
一般来说，rebase后的 dev 和远程的origin/dev会发生分离，在命令行界面中会提示：
```bash
Your branch and 'origin/dev' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)
```
这时需要用git push -f强制推送，覆盖远程分支。若使用了提示中的git pull，结果会变成合并，并产生一个合并提交点。

慎用git push -f!