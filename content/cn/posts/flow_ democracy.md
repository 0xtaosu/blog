---
title: "论区块链的流民主"
date: 2019-12-08T22:47:22+08:00
draft: false
---
从民主谈起，谈到民主，不得不谈投票，投票是民主的特色，投票有三种机制，直接民主、间接民主，以及流民主。

直接民主，即一人一票决定议题，但是也受限于选民的知识水平和政治素养。直接民主是一种自古存在的民主体制，常被认为首见于原始社会，典型例子是是古希腊的“公民大会”。直接民主优点是反应了选民最原始、最真实、最纯粹的态度，但是缺点是投票率低、受限于选民的知识水平和政治素养，容易导致多数人对少数人的暴力。典型例子是纳粹德国的上台。

间接民主，即先投票选择代表，再由代表投票决定议题，存在代表不作为甚至作恶的可能性.。间接民主起源于13世纪的英格兰，其标志是英格兰议会的形成。间接民主现代世界各国普遍实行的基本政治制度和政权组织形式。间接民主优点是可实现、更专业、更理性、能够很好的维持民主制的国家机器运转，但是缺点是选举出来的代表可能脱离群众、不作为甚至作恶。

流民主，即针对某个议题，可以直接投票，也可以把投票权委托给一个代表，再由这个代表投票决定这个议题，但是执行过程非常复杂。流民主起源于Bryan Ford在1884年发表的论文《Delegative Democracy》。在互联网时代，流民主也开始有些有趣的实现，典型例子是Google员工通过Google Votes决定今天吃什么，如果某人不知道今天要吃什么，他先把决定权委托给口味相近的同事，再由这个同事决定今天吃什么。流民主的优点在于对直接民主和间接民主的折衷，既保证了足够真实、纯粹的民主，也提高投票率、能够专业、理性去解决问题。但是流民主的执行过程非常复杂，需要频繁的、实时的统计投票权。因此，现阶段流民主更多还是一种政治学上的假想而没有被采用。

![result](/img/论区块链的流民主/1.png)

随着区块链技术的出现，尤其是DAO的出现，流民主开始具备市场可行性和技术可行性，但仍然存在实时的统计投票权的时间复杂度过大的问题。

投票是区块链技术的常见应用场景。根据CNN报道，2018年5月初，美国西弗吉尼亚州初选中在两个县测试了区块链在线投票技术。链上投票优点在于，开放性、透明性、隐私性和程序化计票，缺点在于用户使用门槛较高。

DAO被称之为去中心化自治组织，在DAO 中的每个人都可以发布提案并进行投票来做决策。DAO是一个计算中的社会实验，它本质上还是一个社交网络，映射了现实世界中错综复杂的利益网络，它通过机制设计、使用智能合约平衡网络中每个人的利益。投票是DAO一个核心环节，DAO可以尝试多种投票方式，直接民主、间接民主，甚至是流民主。

DAO很适合采用流民主，流民主可以实现实时计票，但是如果采用传统的图遍历算法，时间复杂度为O(n)。举个例子，在一个采用流民主的DAO中，每一个节点都有投票权，其投票数等于其序号，箭头方向代表委托方向。在一次投票中，可以有，节点1有投票数66，投票给A;也可以有，节点5有投票数11，不再把投票权委托给节点4，直接投票给B，同时节点1有投票数55，投票给A。在流民主的DAO中，其委托关系是一个树，为了计算和更新每个节点的投票数，每次投票都需要对这个树进行先序遍历或后续遍历，其时间复杂度为O(n)。

![result](/img/论区块链的流民主/2.png)

ASResearch提出了一种快速算法，可以用O(logN)的方法在以太坊上实现流民主投票。该算法的两个关键技术分别是默克尔树（Merkel Tree，一种链上存储方法）和线段树（一种数据结构）。它主要包括以下流程：

1. 在投票开始阶段，每位投票者先获取链上得委托关系图，然后在链下初始化数据；
2. 在投票阶段，每位投票者不允许修改其委托关系，需要计算投票权，在投票的同时的提交到链上。投票合约会用默克尔树的方法（时间复杂度为O(logN)）来验证其初始化信息是否正确；
3. 投票合约则通过线段树来实现时间复杂度为O(logN)的投票状态的更新和查询。

其中，投票状态的更新和查询的流程如下：

1. 计算投票者的已损失票权，即其孩子节点中已投票节点的总票权和；
2. 该投票者的实际票权t为其总票权减去其已损失票权，同时t也是其候选者此次获得（增加）的票权；
3. 找到该投票者的最近投过票的父节点，更新其所投票的候选人的票数（减去t）；
4. 更新所有该投票者的孩子节点的最近投票父节点信息；
5. 更新从该投票者到其最近投过票父节点的路径上的所有投票者的已损失票权（增加t）。

下图是在以太坊测试网中的实验结果，其中横坐标为投票者数目n，纵坐标为消耗gas数目，虚线为最大gas限制。结果表明用传统算法当n达到1000时已经超出了限制，而快速算法在n等于3000时gas消耗仍然维持在一个很小的值，符合理论估计结果。

![result](/img/论区块链的流民主/3.png)