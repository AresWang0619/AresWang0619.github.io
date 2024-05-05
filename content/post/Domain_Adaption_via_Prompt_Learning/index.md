---
title: 论文解读 |Domain Adaptation via Prompt Learning
subtitle: 
# Summary for listings and search engines
summary: 2024/2/26 论文阅读

# Link this post with a project
# projects: []

# Date published
date: '2024-02-26T00:00:00Z'

# Date updated
lastmod: '2024-2-28T00:00:00Z'

# Is this an unpublished draft?
# draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: from paper'
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - Ares
  

tags:
  - 论文解读
  - CV
  - Promot Learning

---

**abstract:**
  Unsupervised domain adaption (UDA) aims to adapt models learned from a well-annotated source domain to a target domain, where only unlabeled samples are given. Current UDA approaches learn domain-invariant features by aligning source and target feature spaces. Such alignments are imposed by constraints such as statistical discrepancy minimization or adversarial training. However, these constraints could lead to the distortion of semantic feature structures and loss of class discriminability. In this paper, we introduce a novel prompt learning paradigm for UDA, named Domain Adaptation via Prompt Learning (DAPL). In contrast to prior works, our approach makes use of pre-trained vision-language models and optimizes only very few parameters. The main idea is to embed domain information into prompts, a form of representations generated from natural language, which is then used to perform classification. This domain information is shared only by images from the same domain, thereby dynamically adapting the classifier according to each domain. By adopting this paradigm, we show that our model not only outperforms previous methods on several cross-domain benchmarks but also is very efficient to train and easy to implement.

在进行论文解读之前，我们需要了解一些背景知识。

首先，最重要的是什么是 prompt learning？

简单地说，就是对输入的文本信息按照特定模板进行处理，把任务重构成一个更能够充分利用预训练语言模型处理的形式。

那么，首先我们要知道预训练模型到底做了什么？

预训练模型提供了一个很好的初始化参数，这组参数在预训练任务上的表现很好。但是下游任务种类很多，我们需要在这组参数的基础上进行 Fine-tune 以适应我们的下游任务。目前做 NLP 任务的大致流程即 "Pre-train, Fine-tune"。融入了 Prompt 的模式大致可以归纳成 "Pre-train, Prompt, and Predict"，在该模式中下游任务被重新调整成类似预训练任务的形式。

![传统的预训练模型](/uploads/tradition_pretrained_model.jpg "传统的预训练模型")

传统方法：
1. 输入句子【今天天气真好】。
2. 将句子送入预训练模型，得到句向量。
3. 使用不同的处理方式（如CRF、Softmax平均），将句向量送入全连接层。
4. 将FC层的输出维度设定为二维。
5. 应用Argmax或Softmax，得到概率最大的下标，即积极或消极。

![使用了 prompt learning](/uploads/prompt_way.jpg "使用了 prompt learning")

使用 prompt：
1. 在【今天天气真好】前提问一个问题，例如：“后面的句子情感是积极的还是消极的？”
2. 在问题后面添加一个 MASK，我们期望 MASK 输出是积极的。
3. 如果生成的词是积极情感的，将其映射为标签1；否则，模型继续学习。
4. 无论是积极还是消极，确保生成的词在模型学到的词汇表中存在。

提出背景：

1. 在预训练和微调阶段，不同的优化目标导致性能损失。预训练语言模型适配任务时可能会损失性能。

2. 预训练语言模型体量庞大、训练复杂，难以进行微调。

因此，需要探索更轻量、更普适的方法。Prompt Learning 的出现旨在解决适配下游任务性能损失和微调困难的问题。其目标是使下游任务更适配语言模型，而基于目标工程的预训练语言模型则是让模型适配下游任务。

## introduction：

近年来，深度学习在大规模标注数据的帮助下取得了巨大成功，但标注大规模数据集仍然是一项费时费力的任务。为了克服这一挑战，提出了无监督领域自适应（UDA，Unsupervised Domain Adaptation）的概念：即从注释良好的源域（Source Domain）学习到的模型自适应到只提供未标记样本的目标域（Target Domain）。其核心目标在于在域偏移（Domain Shift）情况下实现知识的迁移。目前，常见的UDA方法主要基于卷积技术，通过调整模型表示，使得源域和目标域的特征空间更加相似，以此来学习域不变表示。

传统的UDA方法分类:
1. 基于统计差异最小化: 最大均值差异（MMD，Maximum Mean Discrepancy)和中心距差异（CMD，Central Moment Discrepancy）
2. 基于对抗学习:通过融合判别器来减少源域和目标域在特征空间的差异。

存在困难：
1. 源域和目标域之间存在数据分布偏移，对齐容易产生源域特征扭曲，类的可分辨性丧失。

2. 由于数据的分布非线性，语义信息和源域信息纠缠，容易产生语义信息丧失。
   
针对这些困难，虽然已经提出了一些改进方法，如保留语义信息以维持类间信息差异，但仍然存在一个问题，即领域对齐和保留语义特征之间的权衡。

为了解决这一问题，提出了学习解耦语义（Disentangled Semantic）的概念，即将语义和域信息分离。为了实现这一目标，引入了Prompt Learning Method for UDA，即通过提示学习实现域自适应。这种方法的优点在于能够学习到在连续标签空间中的表示，从而避免了语义信息的丧失，并实现了领域和类别分离的表示。

本文中的Prompt是由三部分组成：域无关上下文/Domain-agnostic（用来表示任务信息，是共享的，它比较不关注特定领域差异，注重通用理解），域特定上下文/Domian-specific（表示域信息，捕捉特定的领域特征），类标签/Class lable（区分不同的类别，更好地保留语义信息），

![Prompt Learning Method for UDA](/uploads/prompt_inpaper.jpg "Prompt Learning Method for UDA")

