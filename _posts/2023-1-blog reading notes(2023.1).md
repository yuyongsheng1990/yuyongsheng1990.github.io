---
layout:     post
title:      Blog reading notes(2023.1)
subtitle:
date:       2023-1-3
author:     Yongsheng Yu
header-img: img/
catalog: true
tags:
    - blog reading notes
---
Official Accounts: PaperWeekly
## 2023-1-3 ICML2022: GNNRank: 基于有向图神经网络从两两比较中学习全局排序
    来源：The 39th International Conference on Machine Learning (ICML 2022)
    标题：SGNNRank: Learning Global Ranking from Pairwise Comparisons via Directed Graph Neural Networks
    作者：Yixuan He, et al.
    链接：https://arxiv.org/pdf/2202.00211.pdf
    github: https://github.com/SherylHYX/GNNRank


### 内容简介
  - Background: 在分析大规模数据时，通常会寻找各种形式的数据排名(即排序)，来达到识别最重要的条目、有效计算搜索和排序操作或提取主要特征。
  - <font size=3 color=green>challenge: GNN在任务排名中的能力还不够完善。
    - 少数现有作品限于特定设置，例如top-n个性化推荐和近似中心性度量。
    - 另一个技术差距是无法通过直接优化排名目标来学习模型</font>
  - <font color=blue>solution: GNNRank框架，这是一种与现有GNN模型兼容的端到端的排名框架，能够学习有向图的节点嵌入。</font>


## 2023-1-4 一文盘点图数据增广(Graph Data Augmentation)近期进展
![20230104_093421_47](image/20230104_093421_47.png)
  - background: 近年来，以数据为驱动的推理在数据增广技术引入后，模型泛化能力和性能得到了显著提升。
    - 数据增广技术通过创建现有数据的合理变体而无需额外的真实标签来增加训练数据量，并且已在CV和NLP中得到广泛应用。
  - <font color=green> graph data不规则和非欧结构，很难将CV和NLP的数据增广技术直接应用到图领域。
    - problem-1: 特征数据不完整。
    - problem-2: 幂律分布带来的结构数据稀疏性。
    - problem-3: 人工标注的昂贵成本导致标记数据缺乏。
    - problem-4: GNN中消息传递会导致的过度平滑。</font>
  - Data Augmentation strategies,与图像和文本不同，graph data是连接数据，通常是非独立同分布的。无论是节点级、边级、图级别的任务，图增广数据往往会对整个图数据集做出改动。
    - node dropping
    - edge puturbation边扰动
    - attribute masking
    - subgraph sampling子图采样

![20230104_152845_13](image/20230104_152845_13.png)

### G-Mixup: Graph Data Augmentation for Graph Classification
**<font size=3 color=red>新的增广策略</font>**  
<font color=green>problem: 不同图有不同数量的节点、不容易对齐、在非欧几里得空间中的类型学具有特殊性</font>  
<font color=blue>solution: class-level的图增广方法G-Mixup。首先使用同一类中的图来估计一个graphon。然后，在欧几里得空间中对不同类的graphons进行插值，混合不同图类的graphons。基于混合graphons采样生成合成图。经过实验评估，G-Mixup显著提高了gnn的泛化性和鲁棒性。</font>  

![20230104_161155_48](image/20230104_161155_48.png)

**contributions:**
  - 提出了G-Mixup来扩充用于图分类的训练图。由于直接混合图是难以处理的，因此G-Mixup将不同类别的图的图元graphon混合已生成合成图。
  - 从理论上证明合成图是原始图的混合，其中源图的关键拓扑(即判别主题)将被混合。
  - 证明了G-Mixup在各种图神经网络和数据集上的有效性。  

### AutoGCL: Automated Graph Contrastive Learning via Learnable View Generators
**<font size=3 color=red>自动选择增广策略的自动图对比学习方法</font>**  
background: graph contrastive已广泛应用于图表示学习，其中**视图生成器**在生成有效对比样本方面起着至关重要的作用。  
<font color=green>大多数现有对比学习方法采用预定义的视图生成方法，比如node dropping或edge puturbation，通常不能很好地适应输入数据或保留原始语义结构。</font>  
<font color=blue>自动图对比学习(AutoGCL)新框架</font>  
**<font size=3> contributions</font>**  
  - 提出了一个图对比学习框架，其中可学习的图视图生成器嵌入到自动增广策略中。据作者所知，这是第一项为graph contrastive learning构建可学习的生成节点增广策略的工作。
  - 提出一种联合训练策略，用于在图对比学习的背景下以端到端的方式训练图视图生成器、图编码器和图分类器。
  - 本文在具有半监督、无监督和迁移学习设置的各种图形分类数据集上广泛评估了所提出的方法。t-SNE和视图可视化结果也证明了方法的有效性。

![20230104_162337_98](image/20230104_162337_98.png)

![20230104_162405_93](image/20230104_162405_93.png)   

### Bootstrapping Informative Graph Augmentation via A Meta Learning Approach
**<font size=3 color=red>将元学习应用到图数据增广的可学习增广方法</font>**  
<font color=green>大多数增广方法都是不可学习的</font>  
<font color=blue>可学习的图增广</font>因为一个“好的”图增广必须在实例级别具有一致性，在特征级别具有信息量。  
图增广器的目标是促进特征提取网络学习更具判别力的特征表示
contributions：
  - 提出可学习的方法来生成信息图扩充，称为元图扩充，它提高了图对比学习的性能。
  - 提出了一种辅助元学习方法来训练可学习的图形增广器
  - 在基准数据集上进行实验，结果证明了该方法的优越性。

![20230104_163546_72](image/20230104_163546_72.png)

## 2023-1-5 Neural Eigenmap: 基于谱学习的结构化表示学习
    title: Neural Eigenfunctions Are Structured Representation Learners
    linkage: https://arxiv.org/pdf/2210.12637.pdf
    codes: https://github.com/thudzj/NEigenmaps  

  - 可用于自监督学习、图节点表示学习和谱聚类。
  - Eigenmaps是特征函数(eigenfunctions)的输出。这些方法基于图邻接矩阵(graph adjacency matrix)定义一个核，计算其主特征函数，并以其输出作为节点的表示，完成后续的聚类等任务。也被证明能够维持数据流形上的局部邻域结构的最优表示。

  ![20230105_140715_14](image/20230105_140715_14.png)

  - <font color=green>spectral clustering和Laplacian Eigenmaps是非参的，依赖于求解一个矩阵特征值问题得到eigenmaps，不能拓展到大规模训练数据上，也不能高效地执行样本外泛化。</font>
  - <font color=blue>用神经网络作为函数逼近器来近似核函数的主特征函数。</font>
