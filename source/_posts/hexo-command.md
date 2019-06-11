---
title: hexo 的常用命令
date: 2019-06-11 11:43:56
tags: 
---

## 常用 hexo 命令

hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
hexo help  #查看帮助
hexo version  #查看Hexo的版本

## 缩写

hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy

## 组合命令：

hexo s -g #生成并本地预览
hexo d -g #生成并上传
hexo clean & hexo d -g # 清除缓存 生成静态页面并发布



























