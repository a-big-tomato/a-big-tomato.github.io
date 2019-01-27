---
title: 论文阅读——Semi-Supervised Learning Enabled by Multiscale Deep Neural Network Inversion 
date: 2018-03-05 18:41:00
tags:
- semi-supervised learning
- loss function
mathjax: true
---



题目 Semi-Supervised Learning Enabled by Multiscale Deep Neural Network Inversion 

作者 Randall Balestriero

日期 2018年

来源 arxiv

tag:semi-supervised learning;loss function

亮点：作者提出一个通用的loss function 使得任何拓扑结构的DNNs都可以进行半监督学习，同时不需要多余的超参数。

<!-- more -->

主要贡献：

完整的分析论文[1]中的loss function，利用loss-dependent重整化消除超参数

介绍一种新的半监督学习多尺度损失，这个损失函数对初始化、标记数据集的采样以及输入中的噪音呈现具有鲁棒性。

详尽的实验说明了方法的实现了state-of-art的结果

![](https://note.youdao.com/yws/api/personal/file/WEB91702e38e754eca6d4054834208a17f6?method=download&shareKey=04436358e88b909f9c1f7946a4b67c89)

公式：

1.去超参数

原先：

![](https://note.youdao.com/yws/api/personal/file/WEB1703f9217262c26297e2d9ab3e7de275?method=download&shareKey=205c25415c2bcfe784d132d60f161d22)

改进：

![](https://note.youdao.com/yws/api/personal/file/WEB410e208ca5227bd1379d8a02c2c62970?method=download&shareKey=5168f47e29e2c5083b48a90953a9fb21)

2.将全局loss（$Γ$）改为多尺度loss($λ $)

![](https://note.youdao.com/yws/api/personal/file/WEB347ef37938e1b03d3cd3eefd22ac431b?method=download&shareKey=5f0459f2a3f9accd7288e762449e28cd)



![](https://note.youdao.com/yws/api/personal/file/WEBf10f8ca06b186c4e073f852c30767cd1?method=download&shareKey=7ea2f2fdfaeeb448053f5d98c9dcf657)

![](https://note.youdao.com/yws/api/personal/file/WEB1416c1f0261412360623facad8e0c26f?method=download&shareKey=599ae6c87a754dfcd00bc0f7556dd6bc)

因此，文章提出的完整公式为：

![](https://note.youdao.com/yws/api/personal/file/WEB597294593e104f9f33882ab15b3a0c7e?method=download&shareKey=93a2c2e4686845aa67bf1e8ff741708a)

PS，个人认为作者实验的时候，$$\beta = \frac{1}{log(C)},\beta^{(l)}_R = \frac{1}{L} *\frac{1}{D^{(l)}}$$

实验证明：多尺度loss($$λ $$)要比全局loss（$$Γ$$）的表现好

下一步可进行的工作：

可以通过计算需求和模型能力之间的标准折衷来实现进一步改进。

找到使得loss function 更加鲁棒的超参数（$β_{CE}; β_E; (β^{(l)}_R) ^{L-1}_{l=0}$），比如自动更新

考虑batch size & batch 中未标记样本和已标记样本的比率对大规模网络的适应性学习和鲁棒性的影响。

[1] R. Balestriero, V. Roger, H. G. Glotin, and R. G. Baraniuk.Semi-Supervised Learning via New Deep Network Inversion. ArXiv e-prints, Nov. 2017 