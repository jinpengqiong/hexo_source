---
title: git打tag
date: 2020-05-11 17:05:56
tags:
---
> 通常在发布软件的时候打一个tag，tag会记录版本的commit号，方便后期回溯。
### 列出已有的tag
```bash
git tag
```
```bash
Blog King$ git tag
BD2.1.2
BD2.1.3
BD20191213
BD20191219
BD20191220_latest
BDv2.1.0
BDv2.1.1
BDv2.1.4
```
加上-l命令可以使用通配符来过滤tag
```bash
Blog King$ git tag -l BDv2.1.4
BDv2.1.4
```
### 新建tag
使用git tag命令跟上tag名字，直接创建一个tag。
```bash
Blog King$ git tag v1111
Blog King$ git tag
v1111
```
上面创建一个名为v111的tag。使用git tag命令可以看到新增加的tag。

还可以加上-a参数来创建一个带备注的tag，备注信息由-m指定。如果你未传入-m则创建过程系统会自动为你打开编辑器让你填写备注信息。
```bash
git tag -a tagName -m "my tag"
```
### 查看tag详细信息
git show命令可以查看tag的详细信息，包括commit号等。
```bash
Blog King$ git tag
v1111
Blog King$ git show
commit b5e24e4e929e426998950312a7a7a9e3b9d63e8c (HEAD -> master, tag: v1111, origin/master)
Author: Jin Peng <jinpengguan@126.com>
Date:   Sat May 9 23:22:59 2020 +0800

    ok

diff --git "a/source/_posts/javascript-\344\270\255\344\272\213\344\273\266\345\206\222\346\263\241\345\222\214\344\272\213\344\273\266\346\215\225\350\216\267\346\234\272\345\210\266.md" "b/source/_posts/javascript-\344\270\255\344\272\213\344\273\266\345\206\222\346\263\241\345\222\214\344\272\213\344\273\266\346\215\225\350\216\267\346\234\272\345\210\266.md"
```
tag最重要的是有git commit号，后期我们可以根据这个commit号来回溯代码。

### 给指定的某个commit号加tag
打tag不必要在head之上，也可在之前的版本上打，这需要你知道某个提交对象的校验和（通过git log获取，取校验和的前几位数字即可）。
```bash
git tag -a v1.2 9fceb02 -m "my tag"
```
### 将tag同步到远程服务器
同提交代码后，使用git push来推送到远程服务器一样，tag也需要进行推送才能到远端服务器。
使用git push origin [tagName]推送单个分支。
```bash
git push origin v111
```
推送本地所有tag，使用
```bash
git push origin --tags
```

### 切换到某个tag
跟分支一样，可以直接切换到某个tag去。这个时候不位于任何分支，处于游离状态，可以考虑基于这个tag创建一个分支。
```bash
Blog King$ git checkout v1111
注意：正在切换到 'v1111'。

您正处于分离头指针状态。您可以查看、做试验性的修改及提交，并且您可以在切换
回一个分支时，丢弃在此状态下所做的提交而不对分支造成影响。

如果您想要通过创建分支来保留在此状态下所做的提交，您可以通过在 switch 命令
中添加参数 -c 来实现（现在或稍后）。例如：

  git switch -c <新分支名>

或者撤销此操作：

  git switch -

通过将配置变量 advice.detachedHead 设置为 false 来关闭此建议

HEAD 目前位于 b5e24e4 ok
```
### 删除某个tag

- 本地删除
```bash
Blog King$ git tag -d v1111
已删除标签 'v1111'（曾为 b5e24e4）
```
- 远端删除
```bash
git push origin :refs/tags/v0.1.2
```







