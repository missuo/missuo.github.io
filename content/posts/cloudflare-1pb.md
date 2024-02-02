---
title: "Warning of account suspension by Cloudflare"
date: 2024-01-30T14:45:27-05:00
draft: false
tags: [Cloudflare, 1PB]
---

> 我收到了 Cloudflare 企业专属客服的邮件，让我加她的联系方式。结果没想到加了之后，才知道我的帐号存在被封号的风险。

![20240130RZBNSl](https://r2.qwq.mx/blog/20240130RZBNSl.png)

![20240130Qda0ck](https://r2.qwq.mx/blog/20240130Qda0ck.png)

**这是我每个月的用量，平均每天 50T 流量，每个月达到了 1PB，Unique Visitors 更是达到了 1.4 亿，等于是有十分之一的中国人访问了一次我的网站。**

很多网友非常好奇我到底是跑了一个什么项目，怎么样的的一个站点能够达到如此的规模。甚至这几天我的 [推文](https://x.com/m1ssuo/status/1751810633786331166) 引来了很多的关注，甚至有人说我把 CF 薅秃了之类的。

我想在这里做一些解释，这个网站甚至没几行代码。只有一个 HTML 文件，加上 Nginx 的反向代理。从我的 Commit 记录来看，最早是 2021 年 2 月，已经是三年前了。

主要做的是非常简单的事情，就是通过 Nginx 反向代理了 [Telegraph](https://telegra.ph)。这样就可以匿名地上传无限量的图片，虽然有每张图 5M 的限制，但也够用。我自己用的不多，我博客的图片都在 Cloudflare R2。

为了方便网友尝试，我开放了一个公共站点，即公共图床，方便大家去试用。这个站点没有任何的广告，没有任何的收益。过去的三年，每个月也就不超过 10TB 的流量，很正常的浏览量。而在 2023 年 11 月-12 月左右，开始变得越来越疯狂了，我发现每日的流量从 30T 到 50T。本来我也不管，因为其实我的成本只是贡献了一个域名，一台服务器，更何况缓存率是 99.98%，我的服务器本身并不会产生很多的流量。

直到我收到了 Cloudflare 的邮件，我才意识到我应该处理一下这样子的滥用行为，第一时间我将域名解析到了 **1.1.1.1**，暂停了使用。之后我去检查了一下 Nginx 的访问日志，这让我震惊。

![202401302SLp2n](https://r2.qwq.mx/blog/202401302SLp2n.png)

随意找到了一张图片，或者是 Origin 的站点，毫无疑问 99% 都是中文色情网站。这让我感到失望，初衷是希望大家可以利用这个公共图床写写博客或者是分享一些有趣的图片，而不是用来传播色情。而很夸张的是，我发现知名的色情论坛，t66y 也在使用我的图床，甚至有些用户的头像用的正是我的域名。

为了防止被滥用，我修改了一些 Nginx 的配置，例如我限制了一些图片格式，限制了 Origin。24 小时内流量从 50T 降到了 不到 4T。我也在 Cloudflare 的控制面板上设置了一些规则。

我的好朋友 [SteveYi](https://twitter.com/steveyiyo) 也在第一时间私信我，愿意提供 VM。在这里特别感谢小易。直到目前为止，已经迁移到加州的 10Gbps 带宽的服务器，不再依赖 Cloudflare。

![202401308yg7H3](https://r2.qwq.mx/blog/202401308yg7H3.png)

![20240131AeVWsw](https://r2.qwq.mx/blog/20240131AeVWsw.png)

我不知道还能支撑多久，毕竟这样的公益图床站点没有收益，而且还要承担很大的风险，也许有一天会永久关闭，且用且珍惜吧。

感谢 Telegraph 和 Cloudflare 过去提供的免费服务。