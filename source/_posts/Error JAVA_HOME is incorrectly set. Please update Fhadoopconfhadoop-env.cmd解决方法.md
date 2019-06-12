---
title: Error JAVA_HOME is incorrectly set
date: 2019-06-11 11:43:56 
---
在安装、调试、运行Hexo的过程中，出现了以下错误：

**Error: JAVA_HOME is incorrectly set. Please update D:\software\software\hadoop3\hadoop-3.0.2\etc\hadoop\hadoop-env.cmd**

然后找到对应的目录，打开hadoop-env.cmd，发现其中的 JAVA_HOME 是这样的：
![](/images/Error/1.jpg)

然后打开 terminal，查询 java 版本 以及 JAVA_HOME 环境变量：

![](/images/Error/2.jpg)

发现 JAVA_HOME 已正确配置。那么问题究竟出在哪里？
经网上查阅，因为Program Files中存在空格，所以出现错误，只需要用PROGRA~1代替Program Files即可。如图：

![](/images/Error/3.jpg)

或者也可以将jdk装到其他不存在空格的目录下。
