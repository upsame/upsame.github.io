---
layout: post
title: 学习 Markdown 文本标记语言
category: it
tags: [it]
excerpt: 学习 Markdown 文本标记语言
---

> 原创
>2019年10月28日更新

# 学习 Markdown 文本标记语言

## 谁用Markdown ?
Markdown是为哪些使用者设计的？

>首先要确定你是否真的需要Markdown，使用某种工具是为了提高效率或者某种体验的，如果这种工具并不能显著帮你改善体验，那就让它见鬼去吧，哪怕这个工具学起来很简单。

>Markdown是为那些需要经常码字或者进行文字排版的、对码字手速和排版顺畅度有要求的人群设计的，他们希望用键盘把文字内容啪啪啪地打出来后就已经排版好了，最好从头到尾都不要使用鼠标。

>这些人包括经常需要写文档的码农、博客写手、网站小编、出版业人士等等。通常情况下，**网络上**需要进行大量文字输入的地方都可以通过所见即所得的方式排版（比如知乎的答案编辑模式），**本地写作的话则可以使用word这类常用的文本编辑软件**，当然你也可以蛋疼地手工使用htMl标签实现排版效果——而Markdown只是使这一切更方便了一点而已，所以如果你觉得现有文本编辑方式完全够用了，就别费神折腾了（除非你在使用像github这样Markdown作为主流编辑方式的网站）。 

## 我对Markdown的 感想：
>Markdown ，怎么说呢？**本身**不支持注释功能让人很失望。

>**第二**：只能转化为htMl文件，通过一定渠道可以转化为PDF文件，不能转化为Word（可以直接复制粘贴到word，但是格式不好看，想要的效果都没有了）

>**第三**：PDF本身难以编辑，还是Word比较通用，为了保证兼容性（与其他同学的兼容），还是首先选择word编辑吧！

## 我对Markdown的理解
1. Markdown 就是为了展示给人看的吧，别人不能编辑，可是如果我有一个Markdown文件，我刚使用什么软件去查看这个文件排版格式呢?当然是Markdown专用写作软件，或者支持Markdown书写的文章平台。

>我们设想这样一个情景：我想要查看Markdown文件编译出来的格式文件，所以我找到了一款阅读器可以打开文件并阅读，可是我发现错误想要修改，但是编译出的有格式的文件不可编辑，于是我当然想到要编辑Markdown源文件，这样，可以解释为什么Markdown文件至少要包含源文件了。
>
>其实应该有更好的选择，即：包含.Md的源文件和可以阅读的格式文件，在编辑阅读器中点击修改就可以调出源文件.Md进行修改。
> 
> 实现这一功能的软件就是：Typora(其实真正让我选择它的只是因为它好看而且免费\手动微笑。能支持数学公式的编辑，能导出为pdf) 。

2. 
>事实上我们获得的文件夹中只有源文件.Md而已，因为是即时编译的，所以直接能看到效果。
综上所述，只要我拥有一个可以进行.Md文件即使编译的软件就可以很好地打开Markdown 文件和其产生的格式（效果）文件。

>像notepad++等这样的文本编辑器，只具有编辑。Md文件的功能，当然不能奢望他还能看到编辑生成的最后效果文件的样子。（当然，你可以在头脑中想象嘛！）

>你所看到的各种Markdown编辑器显示的样式都是转换为HTML后加上CSS显示的。

## 关于Markdown编辑、编译器的选择：
那么选择哪一款软件呢？  
有道云笔记吗？MarkdownPod 等桌面软件？CSDN?  简书？
作业部落的CMd Markdown，还是马克飞象？

>MarkdownPod等 已卸载
>
>MarkdownPad是适用于Windows的Markdown编辑编译器，免费版不能导出PDF等,付费版需要15 dollars。
>
> 并且，我安装MarkdownPad之后莫名不能用，提示有错，写入的.Md文件不能预览，这还有什么用呢？
所以我果断卸载了。

>其他的Markdown编辑器应该不能免费支持PDF导出吧？
听说Pondoc--“瑞士军刀”要编译汉字需要结合latex引擎，配置复杂，所以还算是放弃使用这些软件吧。
CSDN就可以支持导出HTML文件（纯文本有乱码，带模板的正常）

发现新大陆：
> Marxico 中文名马克飞象，可以PDF导出，可选择汉字，就是颜色微微不同，效果不如HTML好，但是确实相当不错的。
> 
>马克飞象，本地客户端与在线客户端一模一样，所以安装后卸载了。打开chroMe直接访问官网链接就可以了。
> 
>马克飞象提供 10 天的免费试用，之后如继续使用，请购买会员服务。
未购买或者未及时续费，将不能同步新的笔记。之前保存过的笔记依然可以编辑。

作业部落的CMd Markdown 貌似也要会员才能导出。

简书注册需要手机，写作平台很好，对 Markdown 的支持也很棒。

> 最后的选择当然是：支持Markdown的个人博客、简书、CSDN了。

<a href="https://blog.csdn.net/JustinLee2015/article/details/79751848" target="_blank"> 点击这里 </a>查看Markdown写作平台选择。

<a href="https://www.upsaMe.coM/it/2019/10/22/individual-blog-setup.htMl" target="_blank"> 点击这里 </a>查看我的个人博客建设规划。





