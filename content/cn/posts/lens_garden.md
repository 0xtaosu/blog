---
title: "Lens花园"
date: 2022-08-09T00:26:40+08:00
draft: false
---

Lens Protocol 是一个去中心化且可组合的链上社交网络，部署在 Polygon 上，由 AAVE 创始人 Stani Kulechov 创建。它不是一个应用程序，而是一个协议，定义了链上社交网络数据的存储和组织方式，并提供合约和SDK给开发者调用和建立应用程序。它的特点是，

1. 用户所有;
2. 模块化;
3. 可拓展;
4. 可组合.

![result](/img/Lens花园小记/1.png)

Lens有6个基础模块，分别是个人简介(Profile)、内容(Publication)、评论(Comment)、转发(Mirror)、收藏(Collect)、关注(Follow)，还有可以通过Modules的方式进行拓展，允许用户在内容(Publication)、评论(Comment)、转发(Mirror)、收藏(Collect)、关注(Follow)中自定义规则。现在需要白名单才可以创建个人简介(Profile)和Modules。

![result](/img/Lens花园小记/2.png)

个人简介(Profile)是Lens的主要对象，它是一个NFT，一个Profile NFT代表一份用户资料。用户通过Profile NFT确权了所生产的内容，包括内容(Publication)、转发(Mirror)、评论(Comment)和关注(Follow)。一个地址可以拥有多个Profile NFT。和普通 NFT一样，你也可以把它上架 OpenSea， 打包卖掉你在这个网络中积累的社交资产。目前只有向官方申请才能铸造Profile NFT。

当用户关注了一个Profile NFT，他们会得到一个FollowNFT。一个Follow NFT类似一个关注者勋章。用户另外，用户还可以通过FollowModule来自定义规则，当用户关注一个Profile NFT时，会调用Follow Module。也就是说，可以设置一些有趣的Follow Module，如：

1. 付费关注；
2. 白名单关注。

和普通 NFT一样，你可以把它上架 OpenSea，也可以用它参与投票治理。

当用户Collect了一个Publication，会得到一个Collect NFT。用户还可以通过Collect Module来自定义规则，当用户购买了一个Profile NFT，会调用Collect Modules。也就是说，可以设置一些有趣的Collect Module，如：

1. 付费才可以收藏；
2. 一定时间内才可以收藏。

和普通 NFT一样，你可以把它上架 OpenSea，也可以用它参与投票治理。

内容(Publication)、评论(Comment)和转发(Mirror)都是直接存储在用户的Profile NFT中。内容(Publication)有一个ContentURI，链接可以是AR、IPFS等去中心化存储，也可以中心化服务器。评论(Comment)不仅也一个ContentURI，同时也引用了原始内容(Publication)。转发(Mirror)的ContentURI为空，同时也引用了原始内容(Publication)。

另外，用户还可以通过Reference Module来自定义规则。当用户评论(Comment)或转发(Mirror)了一个内容(Publication)，会调用Reference Modules。也就是说，可以设置一些有趣Reference Module，比如：

1. 评论/转发有奖励


