---
layout:     post
title:      Blog reading notes(2022.10)
subtitle:
date:       2022-10-20
author:     Yongsheng Yu
header-img: img/
catalog: true
tags:
    - blog reading notes
---
Official Accounts: 深度学习与图网络
## 2022-10-20
    来源：Proceedings of the 28th ACM SIGKDD Conference on Knowledge Discovery and Data Mining (KDD 2022)
    标题：Graph Neural Networks with Node-wise Architecture
    作者：Zhen Wang, Zhewei Wei, Yaliang Li, Weirui Kuang, Bolin Ding
    链接：https://dl.acm.org/doi/10.1145/3534678.3539387  

### 内容简介
- background: <font color=red>GNN可以为新图寻找最佳架构，挖掘structural information。</font>  
- **idea: 提出一个<mark>搜索节点的最佳GNN架构</mark>，其中参数控制器根据其局部模式决定每个节点的GNN架构。**
- <font color=green>problem: 现有NAS(Neural Architecture Search)方法的直接扩展将线性增加搜索空间的大小和节点数量，这使得它在大规模图上难以处理。</font>  
- **->扩展: 彭浩在FinEvent中提出的intra-aggregator和inter-aggregator还有用来。。。**
- <font color=skyblue size=3>method:提出一个架构，其中架构的每个方面都有一个参数控制器Aggregatioin，**<font color=red>Aggregator首先将节点的本地模式编码为context embedding，然后根据它从搜索空间中进行选择。</font>**
- **<font size=4>conclusion: Node Resolution</font>**可以提高GNN在大规模图上的性能。  
- 三个方面for framework：
  - <font color=red>Depth，深度</font>
  - <font color=red>aggregator，聚合器</font>
  - <font color=red>Resolution，分辨率。即GNN采样了1-hop or 2-hop的邻居节点来聚合它们的消息。</font>  
  - **Notice: 采样对于大图上训练GNN模型是必要的，但不同的分辨率导致不同的计算图和模型性能，2-hop不一定比1-hop要好！**  
  - **邻居采样器: 在每一跳hop中采样固定数量的节点。**
  - **在大多数情况下，采样仅用于训练而不是评估。**

<font color=green>problem-1: 数据集的多样性阻碍了任何基于图卷积的方法。</font>  

<font color=green>problem-2: 应用相同的架构来处理所有节点可能并不令人满意。</font>  

<font color=red>state-1: 因为3-hop通常无法适应GPU内存，更不用说更大的邻域了。</font>
