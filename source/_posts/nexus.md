---
title: 使用nexus建立个人npm库
date: 2017-11-13 23:05:04
tags:
---
下面分享一下如何使用nexus建立自己的npm仓库
## 准备工作
------
- java环境
- node环境
- [nexus安装包 3.6.0](https://sonatype-download.global.ssl.fastly.net/nexus/3/nexus-3.6.0-02-win64.zip)

## 运行nexus
------
进入解压后nexus的bin文件夹，在此目录打开cmd。执行
```
nexus /run
```
默认端口为：[8081](http://localhost:8081/)，打开可以看到nexus界面了。
> 点击右上角可以登录，默认账号密码：admin  admin123

![运行成功的图片](http://owrfhrwdi.bkt.clouddn.com/W4UKA3OGE%5DNO%5D%60NBDQ5%60DVQ.png)
> "箱子"图标就是代表着**仓库中的包**，"齿轮"图标则为**设置**，下面我们进入**设置**

![界面](http://owrfhrwdi.bkt.clouddn.com/TIM%E5%9B%BE%E7%89%8720171114001115.png)
> 之后，我们将关注**"Repository"**和**"Security"**栏目。分别用于**创建/管理仓库和用户**

## 创建npm仓库
------
- 点击**"Create Repository"**
![Create Repository](http://owrfhrwdi.bkt.clouddn.com/TIM%E5%9B%BE%E7%89%8720171114001556.png)
- nexus增加了许多仓库类型，下面我们只关注和**npm**相关的
![仓库类型](http://owrfhrwdi.bkt.clouddn.com/TIM%E5%9B%BE%E7%89%8720171114001609.png)

