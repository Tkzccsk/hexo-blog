---
title: changes_not_staged_for_commit
date: 2019-06-12 12:43:42
tags:
- git
categories: git
---

在使用 git 的过程中，要把当前文件夹下的内容 push 到 changsk 分支，先执行 
```
 git add .
```
![](/images/changes-not-staged-for-commit/1.jpg)
然后执行
```
git commit -m "backup"
```
![](/images/changes-not-staged-for-commit/2.jpg)
最后执行 push 操作
```
git push origin changsk # changsk 是我创建的一个分支
```
然后就收到报错，报错信息如下：
![](/images/changes-not-staged-for-commit/3.jpg)
大概意思是：
```
更新（push操作）被拒绝，因为github服务器上changsk分支的有些内容在本地仓库没有。
```
然后我想起了我昨天在 github 仓库 changsk 分支里面创建了一个 README.md，所以本地仓库是没有的，造成了远方仓库和本地仓库的不一致（精确来说是远方仓库有，但是本地仓库没有），所以 push 之前应该先把远方仓库的内容pull（拉取）到本地，然后才可以进行push。

所以先应该执行
```
git pull origin changsk
```
![](/images/changes-not-staged-for-commit/4.jpg)
然后执行
```
git add .
```
然后执行
```
git commit -m "backup"
```
又收到一个不同的错误
![](/images/changes-not-staged-for-commit/5.jpg)
经过网上查阅，大部分人都说是因为没有执行 **git add .**，但我显然不是这个问题。
原因是我要 push 的本地仓库里面还有另外的clone过来的git仓库，我查看文件夹，就像报错信息里面说的， themes/next（Hexo 的一个主题，也是本网站使用的主题） 里面是我 git clone 下来的一个仓库。
解决办法是删除 themes/next 文件夹里面的隐藏文件夹 .git