---
title: 基于眼底视网膜图像的一些相关课设

# location: leetcode
# address:
#   street: 450 Serra Mall
#   city: Stanford
#   region: CA
#   postcode: '94305'
#   country: United States

summary: 计算机视觉课设
abstract: '知识点汇总积累'

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: '2023-12-21T21:25:00Z'
# date_end: ''
# all_day: false

# Schedule page publish date (NOT talk date).
# publishDate: '2021-07-01T00:00:00Z'

authors: [Ares]
tags: [CV]

# Is this a featured talk? (true/false)
featured: False

image:
  caption: 'from course'
  focal_point: Right


---
# 眼科智能诊断系统相关知识

## 评价指标

### 灵敏度 (Sensitivity)
灵敏度（Sensitivity） = TPR = Recall（召回率） = TP / (TP + FN)

- 与模型性能有关，反映漏报，即阳性但检查为阴性的情况。
- 与测试样本先验分布无关。

### 特异度 (Specificity)
特异度（Specificity） = 1 - FPR
FPR = FP / (TN + FP)

- 与模型性能有关，反映误报。
- 与测试样本先验分布无关。

### 准确率 (Precision)
准确率（Precision） = TP / (TP + FP)

- 与模型性能有关，反映误报。
- 与测试样本先验分布有关，当数据内正负样本极不平衡时，AUC缺乏指导意义，AP更能反映广安，作为补充指标。

## 数据处理

### 数据脱敏
- 移除个人信息、敏感信息，给予隐私数据可靠保护。

### 数据采集
- 注意数据多样性（不同病种、不同医院、不同地区人群）。
- 标注数据获取（由多人标注）。
- 数据量大小、测试集构建。
- 数据预处理（去掉质量低以及无法诊断的图）。
- 可能还要考虑相机型号（绑定不同模型），注意采集人群的年龄、性别、地区的比例。

## 模型设计

### 多标签与多分类结合
- 模型选择：seresnext50，采用多标签多分类相结合。
- ResNext = ResNet + Inception

![Resnext](6e413d6c-69c8-4cd1-a0a6-22e2c522c9bc.jpg)

- 在每个残差块中使用多个并行的分支，每个分支的特征按通道拼接输出。
- SE模块：输出时添加注意力机制，即给每个输出通道预测一个权重，将权重与每个通道输出相乘。
- 进行目标检测，将眼底图像进行区域划分，在进入全连接层之前做好特征拼接。

## 模型评估

- 灵敏度
- 特异度
- AP
- AUC
- Precision

## 性能差异原因分析

- 不同测试集难度不同。
- 不同模型性能不同。

## 测试目的

- 模型在哪些病种上误报多？哪些病种上漏报多？
- 模型对于不同型号相机图像的适应情况，哪些型号上性能下降？
- 图像质量对模型性能的影响有多大？
- 测试集难易程度如何界定，模型在不同难度测试集上的性能如何？
- 多病种同时发生时，哪些病种容易混淆？

## 基于深度学习的其他应用

- 视网膜血管分割
- 基于眼底视网膜图像的身份认证
