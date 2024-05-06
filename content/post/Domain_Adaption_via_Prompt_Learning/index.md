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

**title:** 
Domain Adaptation via Prompt Learning

**institute:** 
Department of Automation, BNRist, Tsinghua University 2Beijing Institute of Technology
3Carnegie Mellon University 4Beijing Academy of Artificial Intelligence

**authors:** 
C Ge, R Huang, M Xie, Z Lai, S Song, S Li, G Huang

**Date:** 
2022.2.14

**link:** 
https://arxiv.org/abs/2202.06687


## 首先我们要知道：

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

## 介绍

这篇文章介绍了一种名为Domain Adaptation via Prompt Learning (DAPL)的新型无监督领域适应方法。传统的无监督领域适应方法通常通过对齐源域和目标域的特征空间来学习域不变特征。然而，这种对齐可能导致语义特征结构的扭曲和类别可分性的丢失。与之不同，DAPL方法利用预训练的视觉-语言模型，将领域信息嵌入到提示中，用于执行分类任务。这种方法不仅在几个跨领域基准测试中表现出色，而且训练效率高、易于实现。

总结来说，文章的主要贡献包括：
首次将提示学习应用于无监督领域适应；
提出在提示中使用领域特定的上下文信息，避免了在领域对齐中损失语义信息；
在Office-Home和VisDA-2017数据集上实现了最先进的性能，将准确度提高了2.5%。



## Method overview
提出了学习解耦语义（Disentangled Semantic）的概念，即将语义和域信息分离。为了实现这一目标，引入了Prompt Learning Method for UDA，即通过提示学习实现域自适应。这种方法的优点在于能够学习到在连续标签空间中的表示，从而避免了语义信息的丧失，并实现了领域和类别分离的表示。

本文中的Prompt是由三部分组成：域无关上下文/Domain-agnostic（用来表示任务信息，是共享的，它比较不关注特定领域差异，注重通用理解），域特定上下文/Domian-specific（表示域信息，捕捉特定的领域特征），类标签/Class lable（区分不同的类别，更好地保留语义信息）。

![Prompt Learning Method for UDA](/uploads/prompt_inpaper.jpg "Prompt Learning Method for UDA")

采用对比进行训练。当图像和文本的领域和类别分别对齐的时候，形成一对正例（positive），其余均为反例（negative）。

1.对比X_s在特征空间中对齐y,即在特征空间中对齐“sketch”和"dog"，学习到它们的特征空间表示。
2.对比X_T  和y,将“sketch”的文本表示从”photo“域中分离。     
3.域和类别的表示分别对齐。论文采用对比语言图像预训练（CLIP）作为backbone，以促进快速学习和对比学习。


![Our method](/uploads/prompt_method.jpg "Our method")

