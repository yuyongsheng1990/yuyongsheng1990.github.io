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
## 2022-10-20 KDD2022: 具有节点架构的图神经网络
    来源：Proceedings of the 28th ACM SIGKDD Conference on Knowledge Discovery and Data Mining (KDD 2022)
    标题：Graph Neural Networks with Node-wise Architecture
    作者：Zhen Wang, Zhewei Wei, Yaliang Li, Weirui Kuang, Bolin Ding
    链接：https://dl.acm.org/doi/10.1145/3534678.3539387  

### 内容简介
**<font color=red size=3>核心：挖掘structural information</font>**
- background: <font color=red>GNN可以为新图寻找最佳架构，挖掘structural information。</font>  
- **idea: 提出一个<mark>搜索节点的最佳GNN架构</mark>，其中参数控制器根据其局部模式决定每个节点的GNN架构。**
- <font color=green>problem: 现有NAS(Neural Architecture Search)方法的直接扩展将线性增加搜索空间的大小和节点数量，这使得它在大规模图上难以处理。</font>  
- **->扩展: 彭浩在FinEvent中提出的intra-aggregator和inter-aggregator还有用来。。。**
- <font color=blue size=3>solution:提出一个架构，其中架构的每个方面都有一个参数控制器Aggregatioin，**<font color=red>Aggregator首先将节点的本地模式编码为context embedding，然后根据它从搜索空间中进行选择。</font>**
- **<font color=red size=4>conclusion: Node Resolution 可以提高GNN在大规模图上的性能。  </font>**
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

## 2022-10-21 KDD2022: 同时学习图结构信息和特征信息并具有鲁棒性的图神经网络GNN
    来源：Proceedings of the 28th ACM SIGKDD Conference on Knowledge Discovery and Data Mining (KDD 2022)
    标题：Reliable Representations Make A Stronger Defender: Unsupervised Structure Refinement for Robust GNN
    作者：Li Kuan, Liu Yang, Ao Xiang, Chi Jianfeng, Feng Jinghua, Yang Hao, He Qing
    链接：https://dl.acm.org/doi/10.1145/3534678.3539484  

### 内容简介
**<font color=red size=3>核心：重建--边权重，探讨表征学习</font>**
- <font color=green>problem: 攻击者可以通过恶意修改图结构来灾难性地降低GNN性能</font>
- <font color=blue>solution: 通过学习两个端节点的成对表示之间的度量函数来对边权重进行建模</font>，该函数为对抗性边分配低权重。  
- method: STABLE的无监督pipeline来优化图结构。

### literature review
<font color=black>现有方法使用原始特征或GNN学习的表示来对边权重进行建模</font>  

<font color=green> problem:
- 原始特征不能表示节点的各种属性，e.g. structural information  
- GNN学习的表示可能会受到有噪声图的影响</font>  

<font color=red>idea: 学习编码特征信息和结构信息，并且对结构扰动不敏感的表示</font>  

<font color=blue>solution: STABLE的无监督pipeline来优化图结构，最后将精细化的图输入到下游分类器中。</font>  

### contributions of method
1). 提出了一种具有鲁棒性增强的**<font color=red>对比方法</font>**来获得用于**结构细化的表示**，该方法可以有效得捕获节点的结构信息并且对扰动不敏感。  
2). 探讨了GCN缺乏鲁棒性的原因，并提出了一种更鲁棒的归一化技巧。
3). 在四个真实世界数据集上，STABLE可以防御不同类型的对抗性攻击，并优于最先进的防御模型。  

### Model Architecture
- 结构学习网络  
  - 表示学习。<font color=red>对比学习方法，该方法具有面向鲁棒性的图数据增强，可随机恢复去除的边。</font>
  - 图细化。**然后根据同质假设利用学习的表示来修改结构**
- GCN分类器。通过观察对抗性边连接的节点具有那些属性，本文仔细改变了GCN中的重整化技巧以提高鲁棒性。

#### 表征学习
<font color=red>STABLE 通过利用与任务无关的对比方法和面向鲁棒性的增强来学习表示，从而避免前面提到缺陷。</font>  

1). 相似度预处理。sim(中心节点vi, 邻居节点vj) -> 去掉一些扰动边perturbed graph  
2). 对比方法recover edge。**<font color=red>生成视图</font>**是对比方法的关键部分。图的不同视图为每个节点提供不同的上下文，本文希望本文中的视图携带上下文以增强表示的鲁棒性。增强后图的邻接矩阵 A1 = A + E\* P  
3). 编码器遵循传播规则。Discriminator = s1\*H - s1\*H估  
4). 全局平均池化  

#### 图细化
一旦准备好高质量的embedding表示，就可以进一步细化图结构。  
<font color=red>底层图的强同质性可以帮助GNN在转导分类方面取得良好的性能。</font>  
图细化：减少异性边(连接不同类)，并添加同性边(连接同一类)
- 利用对比学习编码器学习的**表示embedding representation**来测量节点相似度。
- 然后删除相似度分数低于阈值t2的节点的边 <- <font color=red>prune剪枝操作</font>  

### conclusion
本文实验结果表示，当扰动率很高时，这尤其有效。
