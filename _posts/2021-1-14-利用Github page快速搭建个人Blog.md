---
layout: post
title: '利用Github page快速搭建个人Blog'
date: 2021-1-14
author: Bugmaker
color: rgb(255,210,32)
cover: '../assets/imgs/一小时快速搭建个人blog.jpg'
tags: Blog
---

# 利用Github page快速搭建个人Blog

[toc]

## 概述



- 利用Github的Github page功能提供的网页搭建服务
- 利用基于Jekyll开发的HardCandy-Jekyll模板搭建Blog框架
- 利用Markdown写作Blog内容
- 采用Netlify部署网页，加速国内访问



下文将详细阐述搭建Blog步骤，主要分为五个部分。

创建Github page---创建本地资源---修改模板内容---git远程部署---利用Netlify加速访问



## 方案优点（可跳过）



## 搭建Github page

> **创建Github page**---创建本地资源---修改模板内容---git远程部署---利用Netlify加速访问

首先需要一个Github账号，按正常方式注册即可，部分网络环境可能需要科技的力量。



接着创建一个repository，此repository有严格的命名规范，请命名为```username.github.io```

其中```username```为github用户名



这里可以选择点击```Settings```来使用官方的模板，但因为我们想用自己找的模板，所以放弃这个方式。



至此Github page搭建成功，可以通过```https://username.github.io/```来访问你创建的网页。

因为还没有填入内容，应该会出现```404 not found```的提示。

## 创建本地资源

> 创建Github page---**创建本地资源**---修改模板内容---git远程部署---利用Netlify加速访问

我们首先在本地创建blog的所有内容，然后再上传到github



由于看中了```HardCandy-Jekyll```这个模板，所以先下载[HardCandy源码](https://github.com/xukimseven/HardCandy-Jekyll)到本地。如果有其他模板也可以使用，但是最好是```Jekyll```开发的



创建与repository同名的文件夹，将下载的源码放入其中



分析HardCandy-Jekyll的项目结构，其中

- ```assets```文件夹存放相关图片
- ```_posts```文件夹存放博文
- ```_config.yml```为博客相关的全局参数



在```assets```文件夹中可以放置一些图片用于引用

在```_posts```文件夹中可以写作博文，请按照内置的第一篇博文的格式写作，当熟悉项目后可以修改头部的参数



至此，本地资源创建完毕。

## 修改模板内容

> 创建Github page---创建本地资源---**修改模板内容**---git远程部署---利用Netlify加速访问

其实此时已经可以部署网页了，但是该网页为内置的网页。

我们可以先修改后再部署网页。



打开```_config.yml```文件，根据需要更改相关参数

个人的实践是

- 将```nav```中中文标签更改为英文，如将“主页”更改为"Home"
- 将```portraits```更改为个人照片
- ```SNS-icon```该行不需要修改，如果有不用的联系方式，将下面具体的行用#号注释即可
- ```friends```可以放置友情链接，如果觉得本文帮到了您，可以添加我的主页: )
- ```disqus```评论和```Gitment```评论在国内使用不方便，可以将状态置为```false```

## git远程部署

> 创建Github page---创建本地资源---修改模板内容---**git连接远程部署**---利用Netlify加速访问

如果不采用远程部署，可以直接将代码上传到创建的repository中，但是如果常使用github，建议还是学习一下利用git远程部署



首先我们需要下载git工具，自行搜索教程下载

右键本地的文件夹，点击```Git Bash Here```进入Bash工作台



本地资源和github需要通过ssh进行连接，首先我们需要检查电脑上现有的ssh key

```cmd
$ cd ~/.ssh
```

如果已有ssh连接，后续操作您应该都了解。如果没有ssh连接，我们就需要创建ssh key

```cmd
$ ssh-keygen -t rsa -C "邮件地址@youremail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):<回车就好>
```

然后系统会要你输入加密串（Passphrase）：

```cmd
Enter passphrase (empty for no passphrase):<输入加密串>
Enter same passphrase again:<再次输入加密串>
```

看到这样的界面，就成功设置ssh key了

接着我们根据图片中的地址找到```id_rsa.pub```文件，复制到剪贴板

打开github的repository，选择settings

选择Deploy keys，起一个名字然后将ssh key复制进去，点击允许```write```权限，确认。



测试ssh连接

```cmd
$ ssh git@github.com
```

如果出现下面的文字，则连接成功

```cmd
PTY allocation request failed on channel 0
Hi bugmaker2/bugmaker2.github.io! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

设置账号信息

```cmd
$ git config --global user.name "username"
$ git config --global user.email "user_email@youremail.com"
```

就可以成功连接github了

依次执行下列命令

```cmd
git add *
git commit -m "一些提交信息"
git push -u origin master
```



代码上传后，即可通过```https://username.github.io/```访问网页，更新完资源大约等待5-10分钟后即可看到网页内容。

## 利用Netlify加速访问

> 创建Github page---创建本地资源---修改模板内容---git连接远程部署---**利用Netlify加速访问**

## 致谢

感谢@Huangxy-Minel学长，学长优美的个人主页引发了我搭建blog的想法

感谢@xukimseven提供的Jekyll模板

在搭建过程中，阅读了很多其他搭建blog的博文，感谢所有充满分享精神的人们。