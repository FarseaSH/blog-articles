---
title: "利用Kindle阅读网络文章"
date: 2022-01-03T12:43:06+08:00
updated:
copyright: true  # 暂不支持
category: 经验
tags:
    - 工具
toc: true
toc_fold: false
draft: false
---

在前不久闲鱼公布的 2021 年度十大“无用”产品中，电子书名列第3上榜。Kindle 作为墨水屏幕电子书的代表产品，在许多人生活中使用率并不高，常处于“吃灰”的状态。因为其较小的屏幕，以及流式操作逻辑（无法方便进行前后翻页的对比阅读），并不适用于专业书籍文章的阅读。唯一较好的使用场景是娱乐阅读，例如网络小说，文学作品的阅读。所以，Kindle 常常被戏称为”盖泡面神器“。

现在网络时代信息爆炸，在刷手机时候，其实我们常常会接触到各类文章，微信公众号文章，新闻app时事文章，知乎各类新知文章。但细想起来，对于这些手机上刷到的文章，我个人经常只是扫了一眼过去。手机上阅读很难有沉浸感，很难在手机上专注仔细品读文章。后来想到能否将手机上刷到的文章发送到 Kindle 进行阅读，经过我一番调研和实践，找到一个利用 Inspaper 的解决方案，本文记录一下最后的实现方案。

<!--more-->

## Send to Kindle

在讲 Inspaper 之后，我们可以先看看常用的方案 Send to Kindle。其实，很早之前，就有提供文章发送到 Kindle 服务的各种产品，我印象中有什么狗耳朵，kindle4rss 等等，甚至微信上也有亚马逊官方服务号提供 Send to Kindle 服务。都是这些服务都以单篇文章为单位向 Kindle 投送，即一篇文章作为一个文件。如果一次性想要阅读的文章过多，那么 Kindle 上就会过多的零散小文件，这给后期整理删除带来了不便。有没有一种便捷的方法，可以将这些想要阅读的零散的文章，整合到一个文件，发送至Kindle？很幸运，Instapaper提供了免费的解决方案。

## Instapaper

[Instapaper](https://www.instapaper.com/)是一家提供“稍后阅读”服务的网站，其 slogan 为"Save Anything. Read Anywhere"。简单来说，你可以将浏览过程中，遇到的好网页，暂存到Instapaper，之后使用Instapper app或者网页端进行阅读。

当然，Instapaper也提供了我们所需要的将文章发送到 kindle 的功能。与之前讨论的Send to Kindle不同的是，Instapaper会讲你所有（免费版会有一定的数量限制）暂存的文章，打包整合成一个文件发送到Kindle上。除此之外Instapaper还提供定时发送功能，就我自己而言，我设置成晚上11点将我白天所想看的暂存的文章发送到kindle，方便我进行睡前阅读，这一套流程自己体验还挺不错的。

## 文章暂存操作

如何将看到的好文章方便的暂存到Instapaper，这里我分几种场景进行讨论一下。

**电脑端浏览器网页：**Instapaper提供浏览器插件（Safari & Chrome 都支持），可以一键暂存当前浏览的网页。

**手机端浏览网页（仅以iPhone为例）：**可以安装Instapaper App，其后通过苹果自带的分享将网页暂存至Instapaper。

![Safari中发送文章到Instapaper实例](https://s4.ax1x.com/2022/01/03/THFTUJ.png)

**微信公众号文章：**因为微信的生态较为封闭，微信公众号文章没有直接苹果分享的入口。这里我找到了一个替代方案：先复制公众号文章链接，然后通过快捷指令进行处理。

关于快捷指令的处理，有两种方式，一种是原生App自带的命令，另外一种利用Instapaper提供的Api。在我使用过程中，我发现前者不是特别稳定，所以我使用了后者。我把两种方法实现的脚本贴到下方。注意Api实现的方法需要将用户名username和密码password作为get参数传递，使用时需要修改成自己账户所对应的账号密码。

![快捷指令脚本（左为Api，右为Instapaper原生指令）](https://s4.ax1x.com/2022/01/03/THkQGn.png)

## 后记

以前自己睡觉前常想看点什么，喜欢刷手机度过，受各个App推荐系统的影响，总是刷到很晚，耗尽最后一滴力气才睡觉。其实这样我感觉挺影响睡眠质量的，一是睡眠时间减少了，二是手机蓝光也有一定的影响。现在睡前基本上都是看 Kindle度过的，安安静静的阅读，伴随着文章带来的充实感入睡，一切都更加安定。

关于Instapaper，这里给出的方案都是免费的。除了发送到Kindle的功能，Instapaper自身也是款不错的阅读软件，包括提供的沉浸式阅读体验，笔记标注等等，也希望大家多多发掘，支持优秀的产品。