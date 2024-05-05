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
abstract: >
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

![使用了 prompt learning](/uploads/prompt_way.jpg "传使用了 prompt learning")

使用 prompt：
1. 在【今天天气真好】前提问一个问题，例如：“后面的句子情感是积极的还是消极的？”
2. 在问题后面添加一个 MASK，我们期望 MASK 输出是积极的。
3. 如果生成的词是积极情感的，将其映射为标签1；否则，模型继续学习。
4. 无论是积极还是消极，确保生成的词在模型学到的词汇表中存在。
