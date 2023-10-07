---
title: 教程其二之git
date: 2023-08-04 17:42:16
tags:
  - software-engineering
comments: true
categories: recruitment
---

## 开源为王- git安装与github初入门

“开源（open source）”——人人可审查、修改与增强，可以从这篇文章稍作了解[什么是开源？](https://zhuanlan.zhihu.com/p/27501070)。
至于git——世界上**目前最先进**的分布式版本控制系统，详见廖雪峰大佬的[Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)。

以下内容不对其上概念和重要性做过多阐述，请自行选择阅读上述文章，以下仅从安装配置讨论。

<!-- more -->

## Git 

### 安装

Windows 上安装方法有几种，对于新手推荐以下两种。

#### 官网安装

官网下载地址（通过科学上网访问）：<https://git-scm.com/download/win>
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041758468.png)
> 小提示：如果你对你的英语水平不自信，edge/chrome浏览器可以安装`沉浸式翻译`插件。
官网安装的详细步骤详见[Git详细安装教程](https://blog.csdn.net/mukes/article/details/115693833)

#### Github Desktop 安装

该安装程序包含图形化和命令行版本的 Git。它也能支持 Powershell，提供了稳定的凭证缓存和健全的换行设置。前往 Github for Windows 网站下载，网址为<https://desktop.github.com/>。

### 配置

打开 Git Bash ，命令行界面如下：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041813146.png)

配置用户名：
``` bash
git config --global user.name "username" // 将"username"替换为你的账户名
```
邮箱：
``` bash
git config --global user.email "user@email.com" // 将"user@email.com"替换为你的邮箱
```
> 如果你不清楚为什么要配置用户名和邮箱，请重新阅读[Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)并找到相关部分。

以上命令执行完毕后，可以用如下命令查看配置是否正确。
``` bash
git config --global --list
```
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041817797.png)

确认完毕后，输入：
``` bash
ssh-keygen -t rsa
```
此时有三个配置问题，第一次使用保持默认配置即可，**请连按三次回车键**。
结束后你可以看到两个目录地址，如你保持默认配置则前往系统盘目录`C:\Users(用户)\"username"\.ssh`文件夹查看 ssh 文件是否生成成功，分别为`id_rsa`和`id_rsa.pub`。
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041826736.png)

此时 git 的配置暂时告一段落，让我们将目光转向 github ，世界上最大的开源仓库平台。

## Github

### 注册

如果你对注册账号的流程抱有疑问，请查看[注册Github账号详细教程](https://zhuanlan.zhihu.com/p/616594520)，本博客不再详述。
> 如若可以，建议用非 qq 邮箱注册，出于 qq 号可能被封禁考虑。

你的 github 主页如下：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041832965.png)

### 绑定 git

点击右上角你的头像，选择`Settings`：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041833037.png)

于左侧`Access`下选择`SSH and GPG keys`：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041835639.png)

点击`New SSH Key`：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041840544.png)

title随意取好，个人建议为`你的电脑型号-Windows`（如`ThinkBook16p-Windows`），方便日后管理不同电脑/虚拟机/系统的 git 密钥。 Key Type 保持不变为`Authentication Key`。将**公钥（`id_rsa.pub`）**文件中的内容用 vscode 打开后复制粘贴到key中，然后点击`Add SSH key`即可。
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041841111.png)。

> 如果你对 SSH 公钥与私钥之分很感兴趣，可以阅读[理解公钥与私钥](https://songlee24.github.io/2015/05/03/public-key-and-private-key/)

测试一下你的配置是否成功，在 Git Bash 终端中输入：
``` bash
ssh -T git@github.com
```
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308041848555.png)
看到如上字样则你的 github 与 git 已经配置成功。欢迎来到开源世界！