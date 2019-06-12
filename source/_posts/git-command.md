---
title: git 创建分支
date: 2019-06-12 14:57:14
tags:
- git
categories: git
---

搭建好本地 Hexo ，然后链接到了 github pages，也绑定了域名
[changsk.top](http://changsk.top "我的个人网站") 。但是 github 博客仓库里面中的文件和本地文件不一样，有些差异，这是因为本地文件经 **hexo g** 命令生成静态页面后，然后经**hexo d** deploy（部署）到github上，所以github仓库是没有本地hexo源文件。如果某一天不小心把本地仓库文件删了，或者换了电脑等原因，致使hexo源文件丢失，那么会造成一定的损失。所以可以把本地 hexo 源文件也同步到 github 上面。方法是在原仓库另创建一个分支，专门用于同步本地 Hexo 源文件。

执行以下命令的前提：
**当前主机已经可以通过SSH连接到 github 博客仓库（即本机生成的SSH KEY放入到 github 博客仓库当中去）**

## 新建 git 仓库
首先新建一个文件夹，比如起名为 changsk_backup ，在此文件夹内打开Git Bash，输入命令：
```
git init # 在当前目录创建新的 Git 仓库
```
![](1.jpg)
可以看到在当前文件夹里面会生成隐藏文件夹 .git，表示当前文件夹是一个git仓库

## 添加远程仓库
```
git remote add origin https://github.com/Tkzccsk/changsk.git 
```
https://github.com/Tkzccsk/changsk.git 是博客仓库的地址，获取方式是登录GitHub，找到自己的博客的仓库。远程库的名字就是origin，这是Git默认的叫法，可以起其他名。

查看远程仓库的名称
```
git remote
```
![](2.jpg)
## 下载远程仓库
将GitHub上的博客仓库完全下载下来
```
git pull origin master # 将远程仓库 origin 的 master 分支 pull 到本地仓库
```
## 创建新分支
创建并切换到一个新分支（原来的分支名为master），输入命令：
```
git checkout -b changsk
```
changsk 为新分支名
上述命令相当于两条命令
```
git branch changsk # 创建分支
git checkout changsk # 切换分支
```
## 上传本地hexo源文件到github博客仓库的changsk分支 
这样就在我们的博客仓库中新建了一个名为changsk的分支，接下来把生成的.git文件复制到本地 hexo 仓库中去，现在changsk_backup就没有用了，可以删了。 
接下来我们把 Hexo 本地博客仓库源文件中上传到GitHub的博客仓库的changsk分支中。

```
git add .
git commit -m "backup"
git push origin changsk
```
git add . ： 使用它会把工作时的所有变化提交到**暂存区**，包括文件内容修改(modified)以及新文件(new)，但**不包括被删除的文件**
git commit -m "backup" ： 主要是将暂存区里的改动给提交到本地的版本库。-m 表示使用消息参数， “backup” 为 -m 的内容，用来表示这次提交的简要说明。
git push origin changsk ： 将本地仓库的代码推送到changsk分支。

进入到GitHub的博客仓库中，可以发现出现了一个新的分支changsk，并且里面是我们的博客原件。
最好在上传备份之前写一份README.md 文件，作为一项说明（因为这是GitHub建议的）。
通过以上方式，我们就完成了备份啦，下一次更新了博客，首先执行

```
hexo clean & hexo d -g
```
###### 注意：部署本地 Hexo 到 github 用的是 master 分支(__config.yml中的声明)
生成及部署hexo，然后执行
```
git add .
git commit -m "backup"
git push origin changsk
```
进行本地 Hexo 源文件的备份。
参考 ：https://blog.csdn.net/qq_34229391/article/details/82251852