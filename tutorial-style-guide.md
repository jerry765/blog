---
title: 教程其四之编码风格
categories: recruitment
date: 2023-08-23 12:09:39
tags:
- style
---

## google 编码风格

{% cq 罗伯特·马丁（Robert C. Martin） %}
干净的代码既简单又直接。干净的代码读起来像写得很好的散文。简洁的代码永远不会掩盖设计者的意图，而是充满清晰的抽象和直接的控制线。
{% endcq %}

**style guide**，编码规范，又称风格指南。每个较大的开源项目都有自己的风格指南：关于如何为该项目编写代码的一系列规定（有时候会比较武断）。当所有代码均保持一致的风格时，在理解大型代码库时更为轻松。

<!-- more -->

为什么要遵循编码规范？
1. 代码更加干净整洁
2. 代码质量更高
3. 提升代码的可读性
4. 使后续维护更加容易

如今大型软件系统之代码量，早已不是一人之力可以完成，需借助团队的力量。此时就显现出编码规范的重要之处。虽然初期为了适应编码规范需要额外的时间、降低了工作效率，但和日后维护的收益比起来，这些阵痛不值一提。

本篇教程我们主要介绍 Google 开源项目的 HTML/CSS 风格指南的部分内容，同时有一些常用规范（如命名约定，函数约定）。如感兴趣可前往文末链接查看完整内容，本教程大部分引用其中。

请注意，我们不鼓励背诵以下内容。快速阅读，按需查找。

### 先导内容

#### 常用编程命名规范

##### 驼峰式命名法(camel case)

第一个单词首字母小写，后面其他单词首字母大写。

``` c++
int myAge;
char myName[10];
float myHeight;
```

##### 帕斯卡命名法（upper camel case）

所有单词首字母大写。

``` c++
int MyAge;
char MyName;
float MyHeight;
```

##### 下划线命名法

用下划线连接单词。

``` c++
int my_age;
char my_name[10]；
float my_height;
```

## 常用风格指南

### 命名约定

最重要的一致性规则是命名管理. 命名的风格能让我们在不需要去查找类型声明的条件下快速地了解某个名字代表的含义: 类型, 变量, 函数, 常量, 宏, 等等, 甚至. 我们大脑中的模式匹配引擎非常依赖这些命名规则.

命名规则具有一定随意性, 但相比按个人喜好命名, 一致性更重要, 所以无论你认为它们是否重要, 规则总归是规则.

#### 通用命名规则

##### 总述

函数命名, 变量命名, 文件命名要有描述性; 少用缩写。

##### 说明

尽可能使用描述性的命名, 别心疼空间, 毕竟相比之下让代码易于新读者理解更重要. 不要用只有项目开发者能理解的缩写, 也不要通过砍掉几个字母来缩写单词。

``` c++
int price_count_reader;    // 无缩写
int num_errors;            // "num" 是一个常见的写法
int num_dns_connections;   // 人人都知道 "DNS" 是什么

int n;                     // 毫无意义.
int nerr;                  // 含糊不清的缩写.
int n_comp_conns;          // 含糊不清的缩写.
int wgc_connections;       // 只有贵团队知道是什么意思.
int pc_reader;             // "pc" 有太多可能的解释了.
int cstmr_id;              // 删减了若干字母.
```

注意, 一些特定的广为人知的缩写是允许的, 例如用 `i` 表示迭代变量和用 `T` 表示模板参数。

模板参数的命名应当遵循对应的分类: 类型模板参数应当遵循**类型命名**的规则, 而非类型模板应当遵循**变量命名**的规则。

#### 文件命名

##### 总述

文件名要全部小写, 可以包含下划线 (`_`) 或连字符 (`-`), 依照项目的约定. 如果没有约定, 那么 “`_`” 更好。

##### 说明

可接受的文件命名实例：
- `my_useful_class.cc`
- `my-useful-class.cc`
- `myusefulclass.cc`

通常应尽量让文件名更加明确.` http_server_logs.h` 就比 `logs.h` 要好。

#### 类型命名

> 如果你还不知道什么是类型，大可以跳过此小节，但我依然建议大致看一下。

##### 总述

类型名称的每个单词首字母均大写, 不包含下划线:`MyExcitingClass`，`MyExcitingEnum`。

##### 说明

所有类型命名 —— 类, 结构体, 类型定义 (`typedef`), 枚举, 类型模板参数 —— 均使用相同约定, 即以大写字母开始, 每个单词首字母均大写, 不包含下划线. 例如:

``` c++
// 类和结构体
class UrlTable { ...
class UrlTableTester { ...
struct UrlTableProperties { ...

// 类型定义
typedef hash_map<UrlTableProperties *, string> PropertiesMap;

// using 别名
using PropertiesMap = hash_map<UrlTableProperties *, string>;

// 枚举
enum UrlTableErrors { ...
```

#### 变量命名

##### 总述

变量 (包括函数参数) 和数据成员名一律小写, 单词之间用下划线连接. 类的成员变量以下划线结尾, 但结构体的就不用, 如: `a_local_variable`, `a_struct_data_member`, `a_class_data_member_`。

##### 说明

###### 普通变量命名

举例：

``` c++
string table_name;  // 好 - 用下划线.
string tablename;   // 好 - 全小写.

string tableName;  // 差 - 混合大小写
```

###### 类数据成员

不管是静态的还是非静态的, 类数据成员都可以和普通变量一样, 但要接下划线。
``` c++
class TableInfo {
  ...
 private:
  string table_name_;  // 好 - 后加下划线.
  string tablename_;   // 好.
  static Pool<TableInfo>* pool_;  // 好.
};
```

###### 结构体变量

不管是静态的还是非静态的, 结构体数据成员都可以和普通变量一样, 不用像类那样接下划线:

``` c++
struct UrlTableProperties {
  string name;
  int num_entries;
  static Pool<UrlTableProperties>* pool;
};
```

#### 常量命名

##### 总述

声明为 `constexpr` 或 `const` 的变量, 或在程序运行期间其值始终保持不变的, 命名时以 “k” 开头, 大小写混合. 例如:

``` c++
const int kDaysInAWeek = 7;
```

##### 说明

所有具有静态存储类型的变量 (例如静态变量或全局变量, 参见 **存储类型**) 都应当以此方式命名. 对于其他存储类型的变量, 如自动变量等, 这条规则是可选的. 如果不采用这条规则, 就按照一般的变量命名规则。

#### 函数命名

##### 总述

常规函数使用大小写混合, 取值和设值函数则要求与变量名匹配: `MyExcitingFunction()`, `MyExcitingMethod()`, `my_exciting_member_variable()`, `set_my_exciting_member_variable()`

##### 说明

一般来说, 函数名的每个单词首字母大写 (即 “驼峰变量名” 或 “帕斯卡变量名”), 没有下划线. 对于首字母缩写的单词, 更倾向于将它们视作一个单词进行首字母大写 (例如, 写作 `StartRpc()` 而非 `StartRPC()`)

``` c++
AddTableEntry()
DeleteUrl()
OpenFileOrDie()
```

### 函数

#### 输入和输出

##### 说明

在排序函数参数时，将所有输入参数放在所有输出参数之前. 特别要注意, 在加入新参数时不要因为它们是新参数就置于参数列表最后, 而是仍然要按照前述的规则, 即将新的输入参数也置于输出参数之前。

#### 编写简短函数

##### 总述

我们倾向于编写简短, 凝练的函数。

##### 说明

我们承认长函数有时是合理的, 因此并不硬性限制函数的长度. 如果函数超过 40 行, 可以思索一下能不能在不影响程序结构的前提下对其进行分割。

即使一个长函数现在工作的非常好, 一旦有人对其修改, 有可能出现新的问题, 甚至导致难以发现的 bug. 使函数尽量简短, 以便于他人阅读和修改代码。

在处理代码时, 你可能会发现复杂的长函数. 不要害怕修改现有代码: 如果证实这些代码使用 / 调试起来很困难, 或者你只需要使用其中的一小段代码, 考虑将其分割为更加简短并易于管理的若干函数。

## HTML/CSS 风格指南

### 总体排版规则

#### 缩进

每次缩进使用两个空格。不使用`TAB`键或混合使用`TAB`键和空格进行缩进。
``` HTML
<ul>
  <li>Fantastic
  <li>Great
</ul>
```

``` CSS
.example {
  color: blue;
}
```

### 整体的元数据规则

#### 编码

使用**UTF-8**无BOM编码。

在 HTML 模板和文档中使用`<meta charset="utf-8">`指定编码。不需要为样式表（css）指定编码，它默认是 UTF-8 。

> 想要了解关于编码的知识，可查阅[unicode 编码简介](https://zhuanlan.zhihu.com/p/137875615)

#### 注释

在需要时尽可能去解释你的代码，包括它的应用范围、用途、此方案的选择理由等。

#### 处理内容

用 **TODO** 标记待办事宜和处理内容。

``` HTML
{# TODO(john.doe): 重新处理水平居中 #}
<center>Test</center>

<!-- TODO: 移除可选的标签 -->
<ul>
 <li>Apples</li>
 <li>Oranges</li>
</ul>
```

### HTML 样式规则

#### 文档类型

使用 HTML5 。HTML5 是所有 HTML 文档的首选： `<!DOCTYPE html>` 。

#### 语义化

根据 HTML 的目的使用它。

根据元素（有时被错误的叫做“标签”）被创造的用途使用他们。比如，对标题使用标题元素，对段落使用`p`元素，对锚点使用`a`元素等。

语义化的使用HTML对于可访问性、复用性和代码的高效性等因素非常重要。

``` HTML
<!-- 不推荐 -->
<div onclick="goToRecommendations();">All recommendations</div>

<!-- 推荐 -->
<a href="recommendations/">All recommendations</a>
```

#### 多媒体降级

为多媒体提供替代内容。

对于图片、视频、通过 `canvas` 实现的动画等多媒体来说，确保提供可访问的替代内容。对于图片，可提供有意义的替代文本（ `alt` ）；对于视频和音频，如有条件可提供对白和字幕。

提供替代内容对辅助功能很重要：没有 `alt` ，一位盲人用户很难知道一张图片的内容，其他用户可能不能了解视频和音频的内容。 （对于 `alt` 属性会引起冗余的图片和你不打算添加CSS的纯粹装饰性的图片，不用添加替代文本，写成 `alt=""` 即可。）

``` HTML
<!-- 不推荐 -->
<img src="spreadsheet.png">

<!-- 推荐 -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

#### 关注点分离

**将结构、表现、行为分离。**

严格保持结构（标识），表现（样式），行为（脚本）分离，尽量使三者之间的相互影响最小。

就是说，确保文档和模板只包含HTML，并且HTML只用来表现结构。把任何表现性的东西都移到样式表，任何行为性的东西都移到脚本中。

此外，*尽可能少的从文档和模板中引用样式表和脚本来减少三者的相互影响*。

结构、表现、行为分离对维护非常重要。更改HTML文档和模板总是比更新样式表和脚本成本更高。

``` HTML
<!-- 不推荐 -->
<!DOCTYPE html>
<title>HTML sucks</title>
<link rel="stylesheet" href="base.css" media="screen">
<link rel="stylesheet" href="grid.css" media="screen">
<link rel="stylesheet" href="print.css" media="print">
<h1 style="font-size: 1em;">HTML sucks</h1>
<p>I’ve read about this on a few sites but now I’m sure:
  <u>HTML is stupid!!1</u>
<center>I can’t believe there’s no way to control the styling of
  my website without doing everything all over again!</center>

<!-- 推荐 -->
<!DOCTYPE html>
<title>My first CSS-only redesign</title>
<link rel="stylesheet" href="default.css">
<h1>My first CSS-only redesign</h1>
<p>I’ve read about this on a few sites but today I’m actually
  doing it: separating concerns and avoiding anything in the HTML of
  my website that is presentational.
<p>It’s awesome!
```

#### type 属性

为样式表和脚本省略 `type` 属性。

引用样式表（除非不是使用CSS）和脚本（除非不是使用JavaScript）不要使用type属性。

HTML5将 text/css 和 text/javascript 设置为默认值，在这种情况下指定type属性并不必要。甚至同样兼容老版本的浏览器。

### HTML 格式规则

#### 常规格式化

对每个块、列表、表格元素都另起一行，每个子元素都缩进。

每个块元素、列表元素或表格元素另起一行，而不必考虑元素的样式（因CSS可以改变元素的 `display` 属性）。

同样的，如果他们是块、列表或者表格元素的子元素，则将之缩进。

（如果你遇到列表项之间有空白的问题，可以把所有 `li` 元素放到一行。Linter鼓励抛出警告而不是错误。）

``` HTML
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>

<ul>
  <li>Moe
  <li>Larry
  <li>Curly
</ul>

<table>
  <thead>
    <tr>
      <th scope="col">Income
      <th scope="col">Taxes
  <tbody>
    <tr>
      <td>$ 5.00
      <td>$ 4.50
</table>
```

### CSS 样式规则

#### id 与 class 的命名

使用有意义的或者通用的id和class名称

用能反映出元素目的或者通用的id、class名称，代替那些很表象的、难懂的名称。

如果名称需要是易懂的，或不容易被修改，应该首选特定的或者能反映出元素目的的名称。

通用的名称适用于非特殊元素或与兄弟元素无区别的元素。他们常被称为“辅助元素”。

使用功能性或者通用的名称，可减少不必要的文档或者模板变化。

``` css
/* 不推荐：无意义 */
#yee-1901 {}


/* 不推荐：表象 */
.button-green {}
.clear {}

/* 推荐：具体的 */
#gallery {}
#login {}
.video {}

/* 推荐：通用的 */
.aux {}
.alt {}
```

#### id与class的命名规范

ID和class命名要尽可能简短，但必要的话就别怕长。

尽可能简洁地传达id或者class名称的含义。

使用简洁的id或者class名称有助于提高可读性和代码效率。

``` css
/* 不推荐 */
#navigation {}
.atr {}

/* 推荐 */
#nav {}
.author {}
```

#### 简写属性

尽可能使用简写的属性书写方式。

CSS提供了多种属性**简写**的方式（如 `font` ），即使只显式设置一个值，也应该尽可能地使用。

使用简写属性有助于提高代码效率及可读性。

``` css
/* 不推荐 */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;

/* 推荐 */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

#### id与class名称分隔符

用连字符分隔ID和类名中的单词。

选择器中的词语和缩写中不要使用除了连字符以外的任何字符（包括空字符），以提高可理解性和可读性。

``` css
/* 不推荐: 单词未分开 */
.demoimage {}

/* 不推荐：使用下划线而不是连字符 */
.error_status {}

/* 推荐 */
#video-id {}
.ads-sample {}
```

### CSS 格式化规则

#### 声明顺序

按字母顺序排列声明。

css文件书写按字母顺序排列的方式，容易记忆和维护，以达到一致的代码。

在排序时忽略浏览器特定的前缀。但是，特定CSS属性的多个浏览器前缀应按字母顺序排列（如-moz书写在-webkit前面）。

``` css
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

#### 块内容的缩进

缩进块内容。

将包括嵌套及声明的 块内容 进行缩进，以体现层次并提高可读性。

``` css
@media screen, projection {

  html {
    background: #fff;
    color: #444;
  }

}
```

#### CSS属性名结束

属性名称的冒号后有一个空格。

为保证一致性，在属性名与属性值之间添加一个空格（但是属性名和冒号间没有空格）。

``` css
/* 不推荐 */
h3 {
  font-weight:bold;
}

/* 推荐 */
h3 {
  font-weight: bold;
}
```

#### 声明块间隔

在选择器和后面的声明块之间使用一个空格。

最后一个选择器与表示 声名块 开始的左大花括号在同行，中间有一个字符空格。

表示开始的左大花括号和选择器在同行。

``` css
/* 不推荐：缺少空间 */
#video{
  margin-top: 1em;
}


/* 不推荐：不必要的换行符 */
#video
{
  margin-top: 1em;
}

/* 推荐 */
#video {
  margin-top: 1em;
}
```

#### CSS代码块分离

使用新空行分离规则。

始终把一个空行（两个换行符）放在代码块规则之间。

``` css
html {
  background: #fff;
}


body {
  margin: auto;
  width: 50%;
}
```

### CSS元规则

#### 分段规则

组的分段由一段注释完成（可选）。

尽可能地用注释来将css分段，段与段之间采用新行。

``` css
/* Header */

#adw-header {}

/* Footer */

#adw-footer {}

/* Gallery */

.adw-gallery {}
```

### 赠言

请与周围保持一致。

如果你正在编辑代码，花几分钟时间看看上下文代码的格式，确定他们的编码风格。如果在上下文代码中，算术运算符前后有空格，或注释前后添加了“#”，你也应该这样做。

编写这个风格指导的目标是让人们可以专注于“我们在讨论什么”而不是“我们该怎么描述”。我们提供了一些通用的编码规范，大家就可以基于这些规范而继续，但特定情况下的规范也同样重要。如果你在一个文件中添加的代码看上去跟其他代码明显不同，你就把阅读此文件的人的节奏打乱了。避免这种情况出现。

## 参考

[Google 开源项目风格指南]("https://zh-google-styleguide.readthedocs.io/en/latest/contents/")