---
title: 教程其一之VSCode
tags:
  - software-engineering
  - frontend
comments: true
categories: recruitment
date: 2023-08-03 11:01:44
---


## 工欲善其事，必先利其器-从环境开始讲起

刚踏入计算机相关专业，却从未有编程经验？甚至从小到大第一次遇见计算机？没有关系，让我们从零开始讲起，一步一步从最最基础的开始讲起。
开篇先叠甲：*以下所有内容仅源于于个人体验，请根据你使用最舒服的方式进行配置。*

<!-- more -->

## 计算机环境

### 科学上网

如题，请确保你能通过**科学上网**访问[Github]("https://github.com/")。如若不能（或者你从未听过科学上网），请询问你身边的学长学姐。

### 安全软件

首先，如果你有良好的计算机使用习惯，日常远离p2p下崽器、xxx中文网，始终对于网络资源尤其是各类安装包保持警惕，安装软件的第一步是寻找官网且日常略过前三广告，那么恭喜你，可以卸载所有安全管家等。**Windows安全中心**绝对足敷使用，请打开它并开启所有必要的保护。
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308021111543.png)
这个可以解决许多因安全软件拦截而产生的疑难杂症。**请务必确保您的使用习惯足够良好，本站概不承担因卸载后猪脑过载导致的财产损失。**

### 浏览器和搜索引擎

Chrome，Edge，Firefox三选其一（排名分先后）。
**近乎所有的国产浏览器都是Chromium套壳+捆绑广告，请不要让它们污染你重金购入的电脑。**
利用科学上网手段注册账号后，打开密码自动填充并在手机端下载相同浏览器，上网体验如德芙般丝滑。
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308021121569.png)
请将默认浏览器设置为你最喜欢的御三家之一，搜索引擎推荐google/bing（前者更好，但需要保持科学上网）。**作为高质量大学生，请不要使用百度搜索引擎。**

益智小游戏，请指出图中真正的steam官网：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308021126585.png)

最基本的计算机环境已经配置完毕，电脑已经清爽许多，现在让我们叩开编程的大门，不妨先从环境入手。

## Visual Studio Code：免费开源的轻量级代码编辑器

### 为什么是 VS Code ？

VS Code 的全称是 Visual Studio Code，是一款开源的、免费的、跨平台的、高性能的、轻量级的代码**编辑器**。

何为编辑器？何为IDE？
- IDE（Integrated Development Environment，集成开发环境）:一组集成在一起的工具，包含文本编辑器、编译器、构建或集成、调试。侧重于工程项目，比较臃肿笨重。如Visual Studio、IDEA、Eclipse。
- 编辑器：文本（代码）的编辑。如Windows系统自带的记事本就是最简单的编辑器。

微软有两种软件：一种是 VS Code，一种是其他软件。

### VS Code 的特点

- 跨平台：支持 MacOS、Windows 和 Linux 等多个平台，且有一致的用户界面和开发体验，支持同步配置
- 开源：源代码、开发计划和发布管理均开源
- 自带终端、Git版本支持
- 丰富的插件拓展
- 活跃的社区生态
- 语法支持：语法高亮、代码智能提示和补全、括号匹配、颜色区分、代码片段提示

### 官网安装

免费？不是70r吗？

![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308021130466.png)

![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308021132921.webp)

这就是为什么推荐google或bing搜索引擎，因为你真的能在国产搜索引擎看到这些。如果对是否是官网有疑问，请尤其注意他的域名。通过域名，能够分辨一大半的虚假官网。

真正的VSCode官网：<https://code.visualstudio.com/>，点开后你应该能看到如下网页。
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308021137406.png)

请根据你的电脑型号（Windows or MacOS）选择对应Stable（*稳定）版本下载。安装过程不再赘述，其中注意Win本**尽量选择安装路径为非C盘**即可，否则后续很可能**因为C盘爆满，Windows系统无法更新**。

安装完成后打开软件，界面如下：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308030942879.png)

如果你对英文界面感觉不太好，那么第一步就是**将VSCode设置为中文**。以下有两种方法：
- Windows用户快捷键`Ctrl+Shift+P`（Mac用户快捷键`Cmd+Shift+P`），打开命令面板，输入`Configure Display Language`，选择`Install additional languages`，然后安装插件`Chinese(Simplified) Language Pack for Visual Studio Code`即可
- Windows用户快捷键`Ctrl+Shift+X`，打开拓展页面，同样安装此插件`Chinese(Simplified) Language Pack for Visual Studio Code`
安装完成后，重启 VS Code 。

解放右手，请熟记常用快捷键组合。

### 常见操作&使用技巧

#### 1、快速生成HTML骨架

新建一个.html文件（如example.html），然后通过以下方式可快速生成HTML骨架：
1. 输入`!`（英文感叹号），然后按下`Enter`键
2. 输入`html:5`，然后按住`Tab`键
生成的骨架如下：
``` HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

**小技巧：**在HTML文件中输入`lorem`可生成一段占位文本。

#### 2、并排编辑：上下左右显示多个文件窗口

Windows用户按住快捷键`Ctrl + \`（反斜杠，在你的`Enter`回车键上方），即可同时打开多个编辑器窗口，进行并排编辑。按快捷键`Ctrl + 1`切换到左侧窗口，`Ctrl + 2`切换到右侧窗口，以此类推。

![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308031012609.png)

### 部分插件推荐

#### 安装插件

![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308031015953.png)

我们可通过点击上图中红框部分，即可在顶部输入框中查找想要安装的插件名，然后进行安装。安装完毕后部分插件会需要重启软件，插件才会生效。
另外，我们也可以通过访问官网的插件市场来安装插件：
VS Code 官网插件市场：<https://marketplace.visualstudio.com/vscode>

#### 推荐的插件

##### 0、基本插件

###### Chinese (Simplified) Language Pack for Visual Studio Code

中文语言插件，不必多言。

##### 1、Git相关

还不熟悉Git？没事，先安装再说，后续我们一定会讲到or用上。

###### GitLens

Git管理神器，可视化仓库。

###### Local History

维护文件的本地历史记录，妈妈再也不用担心我代码忘记保存了。

##### 2、代码显示增强

###### highlight-icemode

选中相同代码时高亮显示。安装后请关闭 VS Code 自带高亮，于用户设置添加`"editor.selectionHighlight": false`。

###### TODO Highlight

什么，手上的 bug 还没修完突然有事，正巧这时候有了思路？按照代码规范，可以在代码中加上 TODO 注释（区分大小写）。
``` HTML
// TODO:发现跳转bug，可能的解决思路为：······
```
或者
``` HTML
// FIXME: 如没有万分把握请勿删去此行注释，可能导致程序崩溃。
```
安装此插件后，打开命令面板（还记得快捷键吗？）输入`TODO-Highlight`，选择相关命令，我们就可以看到 todoList 清单。

##### 3、图片相关插件

###### Polacode-2022

可优雅地分享你的代码截图，如下所示：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308031036600.png)

我们谴责愚蠢的拍屏主义者，`Win+Shift+S`截图为可接受的。

##### 4、Markdown相关

本网站所有博客均由 Markdown 写成，其优点在于不用操心格式，随想随写，解放右手。推荐 VS Code + Markdown ，最好的笔记组合。

###### Markdown Preview Github Styling

以 Github 风格预览 Markdown 样式，简洁且优雅。左侧书写右侧预览。
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308031047619.png)

##### 5、通用工具

###### Live Server 

在本地启动服务器，代码修改时实现**热更新**，不需要手动刷新页面。
使用方式：于代码页面点击右键，选择`Open with Live Server`。

###### WakaTime

统计在各安装了 WakaTime 插件的编程环境中写代码的时间，发现真实的自己。网站统计效果如下：
![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308031051230.png)

##### 6、软件主题

想给你的 VS Code 换个皮肤？欢迎来到海澜之家！

- Dracula Theme

- Material Theme

- Nebula Theme

- [One Dark Pro](https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme)

- One Monokai Theme

- Monokai Pro

- Ayu

- [Snazzy Plus](https://marketplace.visualstudio.com/items?itemName=akarlsten.vscode-snazzy-akarlsten)

- [Dainty](https://marketplace.visualstudio.com/items?itemName=alexanderte.dainty-vscode)

- GitHub Plus Theme：白色主题

- Horizon Theme：红色主题

### 多端协作： VS Code 云同步

1. 上方菜单栏选择`文件-首选项-打开设置同步`
2. 选择需要同步的配置，全选即可
3. 通过 GitHub 账号登录
4. 同步完成后，菜单栏显示“设置同步已打开”

什么，你还没有 [GitHub](https://github.com) 账号？注册啊！

## 写在最后

![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308031041381.jpg)

## 参考链接

[Web-Master/00-前端工具](https://github.com/qianguyihao/Web/blob/master/00-%E5%89%8D%E7%AB%AF%E5%B7%A5%E5%85%B7/01-VS%20Code%E7%9A%84%E4%BD%BF%E7%94%A8.md)
多有参考，如想进一步了解 VS Code 如快捷键及更进一步的配置，可阅读全文。
[为什么要学Markdown？有什么用？](https://zhuanlan.zhihu.com/p/92312642)