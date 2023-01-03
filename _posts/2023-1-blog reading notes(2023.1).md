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
## 2022-1-3 ICML2022: GNNRank: 基于有向图神经网络从两两比较中学习全局排序
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
