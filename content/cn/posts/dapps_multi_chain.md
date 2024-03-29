---
title: "要致富，先修路"
date: 2021-06-05T00:31:03+08:00
draft: false
---

![Multichain](/img/Multi-chain时代下的DApp碎片化/Multichain.png)

去年，以太坊生态繁荣，创新不断，包括DeFi、NFT和Metaverser。但由于以太坊性能瓶颈，交易费用高昂，因此，各dapp需在中心化、安全性和性能中权衡，选择合适的layer2或公链部署。例如，DEX和借贷类DApp（如uniswap）主要部署在主网或rollups，而NFT、游戏（如Dark Forest）倾向于侧链或EVM兼容公链，就像现实世界中，银行和投资公司会聚集在市区，游乐园会被放在郊区。

随着各layer2和公链生态兴旺，DApp和其资产在各链间分散，造成DApp生态碎片化，并影响了DApp的可组合性。由于各链相互独立，同一DApp的状态和资产状态存在差异。例如，DApp的资产流动性在各layer2或公链间被切割，就像就像现实世界中，城市与村庄不通路。

为解决流动性碎片化，项目方或社区建立跨链桥。用户在不同侧链应用间转移需先转至主链，再转至另一侧链，产生双倍Gas费用，且需等待两次跨链确认。另一解决方案是跨链流动性池，通过在链间发起大额转账均衡余额。

Connext 提出了标准的跨链状态通道协议，可以被部署到任何 EVM-Compatible 的区块链上。状态通道运营者者与用户共同设立多签地址后，已签名但并未广播的交易可以作为支票在 P2P 网络中被频繁传输。用户可以用最新的支票在多签地址所在的网络中发起链上交易更改链上余额来兑现支票。Connext团队最近还提出一个[Virtual AMM](https://medium.com/connext/solving-the-liquidity-problem-88bde201501#:~:text=have%20to%20solve.-,Virtual%20AMMs,-The%20above%20problem)的解决方案，通过状态通道建立跨链流动性，像uniswap的AMM一样，做市商可以添加/删除流动性和获得交易手续费，交易者可以跨链交换代币。

![Connext](/img/Multi-chain时代下的DApp碎片化/Connext.png)

另外，Axelar则提供了兼容任何公链的跨链交易和配套的消息中继服务。开发者可以使用 Axelar 的跨链通信协议来锁定、解锁和转移不同公链的DApp资产，以及与任何其他链上的DApp进行通信。

再有就是，LayerZero提供了跨链消息传递服务，可以在任何区块链上部署，通过LayerZero的跨链消息传递服务，可以在不同的区块链上发送和接收消息，从而实现跨链资产的转移。

除了流动性碎片化的问题，DApp还面临着正统性碎片化的问题。正统性是一种文化概念，是由[vitalik](https://vitalik.ca/general/2021/03/23/legitimacy.html)提出，由于跨链桥在一个layer2或公链上锁定DApp的资产的同时，也会再另一个layer2或公链上铸造新的DApp的资产，不同版本的跨链桥将会创建不同版本的DApp资产，从而导致正统性破碎。以BTC为例子，就有renBTC wBTC等不同的版本的BTC。

为了解决决正统性碎片化的问题，在多链时代，DApp官方需要考虑多链路线图，一般有两种方案，一是通过建立官方的跨链桥来铸造资产，并占据大部分的跨链流动性，进而实现正统性；二是在layer2或公链上部署DApp并铸造资产，再通过建立跨链流动性池来打通多链资产。

毫无疑问，碎片化问题对DApp是一个挑战，但是，解决这个问题会给DApp带来极大的收益，就像就像现实世界中，要致富，先修路，它可以充分利用不同的layer2或公链的性能或资源的优势，从而提高用户友好度和吸引更多人来玩这个游戏。