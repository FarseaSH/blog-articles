---
title: "优化热榜类RSS feed源"
date: 2022-04-09T17:07:39+08:00
updated:
copyright: true  # 暂不支持
category: 经验
tags:
    - RSS
toc: true
toc_fold: false
draft: false
---

自己个人很喜欢用传统的RSS feed源来获取信息，因为其简洁纯净的风格，可以避免常规app的算法推荐带来的信息茧房，广告与用户评论带来的嘈杂，RSS的集成性，让自己可以只用一个完全自己定制的app接受各种信息，使用体验很棒。但唯独有一类比较重要的信息我自己并没有找到合适的feed源，就是各大平台的热榜（例如，微博热搜，知乎热榜），这些热榜类信息代表时下社会热点，虽然各类热榜或有些许不足，但我认为也是当下需要每日关注的一类信息。

现有的热榜类Rss feed源，以RssHub为例，并不能带来很好的浏览体验，其原因有三：热榜 chanel是以每一条热榜条目为item，每条item在channel出现的顺序并非按照热度顺序呈现，很难定位到头部重点热点内容；而是以热榜条目为item，整个channel内会出现一段时间内容所有的热榜条目，数量庞大；三是传统意义上，Rss item应该以一篇文章为单位，热榜中每条条目单独作为一条item，信息量极小，与RSS阅读器的操作逻辑不符合。

于是，我自己搭建了一个为热榜类信息优化的RSS源，本文记录一下相关过程细节。

<!--more-->

![左图：优化后的热榜RSS Feed；右图优化前的微博热榜RSS Feed](https://s1.ax1x.com/2022/04/09/LiKCfH.png)

## Feed优化

优化后的RSS feed 将多个网站平台的热榜集成到一个channel，每个单独平台的热榜作为单独的一个item，item里面的内容会将热榜的条目按热榜本身的顺序呈现。RSS feed会每一段时间（例如15分钟）更新一次，抓取各个平台的热榜榜单。更新后的榜单，不会以新item的方式加入channel，而是覆盖掉原来对应的item，例如20点15分的微博热搜item，会覆盖掉20点的微博热搜item。

这样优化后，热榜榜单条目以item文章形式展示，保留原榜单顺序；channel内item数量不会增加，固定为热榜平台来源的数量；item内容的信息不再只是热榜条目一行，而是整个榜单，信息密度增加，符合RSS阅读器的操作逻辑；除了解决传统热榜RSS feed源的三个问题外，优化后的Feed还保证了阅读器所浏览的热榜信息的时效性。

## 更多实现的细节

整个Feed源的实现其实很简单，通过Python脚本抓取今日热榜的条目，再通过模版化渲染输出xml，定时推送的到网页服务器上。其中，我们可以利用Github Action，设置cron定时任务，将输出的xml文本commit到github page上，采用公开的public repo完成这套流程并不会产生任何消费。

关于部署，因为热榜源时效上的要求，定时任务频率很高，每隔10分钟更新一次，就会产生一次commit，一天下来会有很多commit，可能会对自己Github contribution产生一定影响。另外，国内网络访问Github可能会出现延迟过高的问题，我是将最后xml文本挂在Vercel上，国内网络访问不会出现问题，对于静态网站，也是免费的服务。

今日热榜网站还会有反爬的限制，数据抓取时候qps不能太高。今日热榜的热榜条目链接，采用了网站内部转链的方式，后期没有访问今日热榜源网站的session，直接访问转链，并不能直接跳转，所以在进行抓取时候不能直接爬下热榜条目url，还需要二次访问来获得源url。如果用request进行http请求发送，后面直接访问`.url`属性即可得到源url。

## demo

现在项目的代码参见https://github.com/FarseaSH/trending-topics-rss，后期我会将接口设计，实现Fork repo后就能实现定制自己的RSS热榜集成源。

现在项目demo的RSS feed地址为[trending-topics-rss.vercel.app](http://trending-topics-rss.vercel.app/)。