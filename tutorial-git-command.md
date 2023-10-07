---
layout: blog
title: 教程其三之常用git命令
date: 2023-08-16 20:11:06
tags:
- git
- software-engineering
categories:
- recruitment
author: youyiBYSKY
---

> 本文由部长代写形成，赞美 youyiBYSKY

# git的仓库管理
git在工程实践中起着举足轻重的作用，能够大大提高开发时版本迭代的效率。  
接下来，本文将简单介绍一下git管理仓库的一些方法。希望阅读这篇博客的萌新能够看懂。  
**~~毕竟不会用git要担心被开除了~~**
![0](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/noob01.png)  
**（图来自runoob.com）**  
本文从三个方面介绍仓库的管理  
- 本地仓库
- 外部仓库
- 仓库的分支管理

<!-- more -->

本文所用到的代码总览
> ```$ git init //仓库初始化  ```  
> ```$ git status //仓库状态  ```  
> ```$ git add //将工作区文件添加到缓存区  ```  
> ```$ git commit -m "(日志内容)"//提交更改到版本库 ```  
> ```$ git push <远程主机名> <本地分支名>:<远程分支名> //push代码到远程仓库```  
> ```$ git pull <远程主机名> <远程分支名>:<本地分支名> //从远程仓库上pull下代码```  
> ```$ git fetch //从远程仓库下载新分支与数据```  
> ```$ git clone <repo> <directory> //从现有 Git 仓库中拷贝项目```  
> ```$ git branch //查看当前git中的分支列表```  
> ```$ git checkout (branchname) //切换当前所在分支```  
> ```$ git merge (branchname) //将指定分支合并到当前分支```  
> ```$ git branch -d (branchname) //删除指定分支```  

> ```$ git log //查看git日志 ```  

## git本地仓库的基础操作
### 本地仓库的初始化
初始化git本地仓库的命令格式如下
> ```$ git init```  
在所选定的文件夹下启动git，在cmd中输入  
> ```$ git init```  

之后返回提示
```
Initialized empty Git repository in "仓库所在文件夹的路径"

```  
![1](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/1.png)  
即可完成仓库的初始化，同时，在该文件夹下会生成一个 **.git** 文件夹。

此时要查看仓库状态，可以输入  
> ``` git status```  

此时会看到已经被初始化的仓库  
![2](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/2.png)
**这只是一个空仓库**
### 本地仓库的管理
#### 文件的工作区导入
在原来的文件夹下面新增一个 **“GitTest”** 文件夹
在所选定的文件夹下导入你所要保存的项目，启动git，在cmd中输入  
> ```$ git status```   

此时可以看到导入的项目文件未提交的git仓库  

``` bash
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        GitTest/ (.git同级文件)

nothing added to commit but untracked files present (use "git add" to track)
```  

#### 文件的暂存区导入

git中将工作区文件导入到暂存区的命令格式如下：  
>```git add <文件名>```  

在cmd中输入  
```$ git add GitTest/（所要添加到暂存区的文件）```  
```（输入$ git add . 可将当前目录下的所有文件都添加到暂存区）```  

此时再查看仓库状态 
![5](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/5.png)  
可以看到工作区中的文件已经添加到了暂存区  

#### 提交文件到版本库  

git中将暂存区文件提交到版本库的命令格式如下：  
>```git commit -m "(日志内容)"```  

在cmd中输入  
> ```$ git commit -m "提交到版本库" ```  

然后可以看到暂存区的文件已经被更新到版本库  

``` bash
[master (root-commit) c868616] "提交到版本库"
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 GitTest/introduction.md
```  

在cmd中再次输入  
> ```$ git status```  

此时可以看到在版本库更新后，缓存区中的内容已经被清空  
![3](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/3.png)

#### 提交更改到版本库
打开上例中的 /GitTest/introduction.md 文件进行如下修改

![7](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/7.png)

查看仓库状态，可以看到git检测到introduction.md已被修改  
![8](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/8.png)  
按照上一段的步骤再次操作（工作区->暂存区->提交更改）即可将项目保存的修改提交到版本库  

## git远程仓库的基础操作
前言：这里稍稍加速一下，本地仓库的分支管理、版本库回溯等操作暂且跳过，就先优先讲解一写远程仓库的基础操作（pull、push）  
  
~~说实话，这种很不负责任的做法，但为了快速上手，我还是把分支管理放在了这一节之后  
**原谅我**~~    

### 新建远程仓库

登录GitHub ,在主页导航栏找到新建，选中“New repository”,  
![9](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/9.png)  
根据引导创建远程仓库  

### 关联远程仓库
在github中找到远程仓库的地址  
![11](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/11.png)  
新建仓库后复制仓库地址，在git中输入  
> ```$ git remodte add origin "远程仓库地址"```  

![12](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/12.png)  
#### git push

git中push代码的命令格式如下：
> ```git push <远程主机名> <本地分支名>:<远程分支名>```  

现在来开始push我们已有的代码
此时尝试直接输入```git push```来push本地代码，会出现以下情况  
![13](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/13.png)  
这里提示当前master分支没有上传分支，并且提示输入  ```git push --set-upstream origin master``` 来建立origin和master之间的流通道  
***（origin是远程仓库的默认名称，master是本地分支的默认名称）***  
如上建立流通道后，打开github中的远程仓库，可以看到本地代码已经上传至远程仓库  
![14](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/14.png)  

#### git pull

git中pull代码的命令格式如下：  
> ```git pull <远程主机名> <远程分支名>:<本地分支名>```  

打开GitHub，将先前上传的introduction.md 文件做一些改动后保存  
**（在GitHub上直接修改代码时记得选择分支，这个会在之后细说）**  
![15](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/15.png)  
在git中直接输入```git pull```  
![16](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/16.png)  
打开本地的introduction.md ，可以看见GitHub上的更改已经同步到本地  
![17](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/17.png)  

## git的分支管理

分支，是将修改的项目整体分叉保存，每个分叉后的分支相互独立，互不影响。
git的分支模型是git的一大 **“绝学”**，几乎每一种版本控制系统都以某种形式支持分支，一个分支代表一条独立的开发线。  
利用分支，可以让多个人同时为同一个项目进行开发。在自己完成工作后，将自己分支上的修改合并到主分支。  
### 查看与新建git分支  

git中查看分支的命令格式如下：  
> ```git branch```  

在默认情况下，本地仓库只有一个 **master**分支，并且该分支是当前分支。  
![18](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/18.png)  
  

git中新建分支的命令格式如下：  
> ```git branch (branchname)```  

现在我们要新建一个 **“moke”** 分支，只需输入：```git branch moke```  
然后再次输入```git branch```来查看所有分支。  
![19](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/19.png)  

现在我们可以看到，我们有了一个新的分支 **“moke”**。  

### 切换git分支  

git中切换分支的命令格式如下：  
> ```git checkout (branchname)```  

现在我们要切换到方才创建的**“moke”** 分支，就只需要输入```git checkout moke```  
![20](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/20.png)  

可以看到，我们现在已经切换到了 **“moke”** 分支。  

现在打开 introduction.md ，删除第二行的内容，然后更新到版本库。  
![21](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/21.png)  
![22](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/22.png)   

此时输入```git checkout mmaster```切换到默认的master分支。
![23](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/23.png)  

再打开 introduction.md ，可以看到在 **“moke”** 中被删除的第二行回来了。  
![24](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/24.png)  
  
这里证明了不同的分支下，同一个项目可以同时开发，而且互不影响。  

### 合并git分支  

git中合并分支的命令格式如下：  
> ```git merge (branchname)```  

**首先先解释一下这个命令：**  
这个分支合并命令是将指定分支合（上面命令格式中的参数）并到当前分支。
  
上文中master分支与 **“moke”** 中的内容并不相同，这里我们要把这**“moke”**分支合并到master分支。  
在git中输入```git merge moke```,可以看到  
![25](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/25.png)  
再打开 introduction.md ，可以看到在master分支中第二行继承了 **“moke”**的状态，也就是被删除了。  
![21](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/21.png)    

### 删除git分支  

git中删除分支的命令格式如下：  
> ```git branch -d (branchname)```  

上面我们将 **“moke”**分支合并到了master中，那么现在 **“moke”**分支没用了，我们就要准备删除这个分支了。  
在git中输入```git branch -d moke```,可以看到 **“moke”**分支已经被删除了  
![26](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-BYSKY/26.png)  

## 附录
* 合并冲突分支
* git clone 与 pull、fetch之间的区别
* git log命令的使用
* git blame命令的使用
* git diff命令的使用
* 远程仓库的使用进阶
* git版本回溯