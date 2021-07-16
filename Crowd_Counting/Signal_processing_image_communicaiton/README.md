# 团队最新研究成果 -- Signal Processing：Image Communication
+ Aichun Zhu, Guoxiu Duan, Xiaomei Zhu, Lu Zhao, Yaoying Huang,Gang Hua and Hichem Snoussi. "CDADNet: Context-guided dense attentional dilated network for crowd
counting" in Elsevier ScienceDirect

## 一、前言
近年来，随着人群计数在流量分析和安全保证中的应用，基于图像的人群密度检测取得了重大进展。许多研究人员一直致力于探索算法和模型，以实现更好的人群计数性能。然而，现有的方法通常主要关注尺度变化或视角失真的问题。这将使这些模型能够很容易地带来背景信息，从而对尺度或背景特征的表示产生不利影响，以及只在某些特定的人群计数数据集上工作良好。如图1-1所示，可以显著削弱背景信息的影响，提高其表示尺度和上下文信息的能力。大规模的变化和复杂的背景会导致人群计数中的巨大错误。为了解 决这些问题并获得准确的计数结果，我们提出了一种新的架构，称为上下文引导的密集注意力扩展网络(CDADNet)。

![1-1](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/1.1.png)

## 二、本文结构

本文所提出的的情境引导的密集注意力扩张网络(CDADNet)的架构如图2-1所示。它由三个组件组成：上下文引导模块、注意力模块和密集的注意力扩展模块。上下文引导模块用于学习上下文感知功能的权重。注意力模块被设计用于从输入的图像中提取注意力信息。此外，还提出了密集的注意力扩展模块来扩大注意力接受场，并提供高质量的密度图。

![2-1](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/2.1.png)

考虑到以前的方法很容易将背景信息带到大的接受域，从而产生质量较差的密度图，因此提出了一种新的注意力模块来削弱生成高密度地图的背景信息。注意力模块由VGG-16的前13层和一个密集的膨胀块(DDB)构建。DDB由三个膨胀的卷积层组成，膨胀速率为1、2、3。如图2-2所示，密集扩张块是密集注意力扩张块(DADB)的基本成分。

![2-2](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/2.2.png)

为了更好地表示输入图像的多尺度信息，在该模型中加入了一个上下文引导模块。如图2-1所示，前端端已搭建完毕，通过预先训练的Vgg-16网络的前13层，并且Vgg-16的输出作为上下文引导模块的输入。因此，该上下文引导模块旨在从Vgg-16特性中构建多尺度的上下文信息。为了克服标准的Vgg-16模型编码相同的接受域这一限制，我们通过执行平均池化和1×1卷积层来利用多尺度的上下文特征。这些多尺度的特征被连接在一起，作为DADB的输入。

我们提出了一个密集的注意力扩展模块，其中包含几个密集的注意力扩展模块 (DADBs)。这些嵌块包含三个扩张的卷积层，膨胀速率为1、2、3。该设 置可以减少由于一系列质数间膨胀而造成的像素信息的损失。具体而言，先前DADB的输出作为对以下DADB的输入，如图2-1和2-2所示。为了防止网络出现太长时间和丢失信息，我们在每个块后面添加了一个注意力生成器，以更好地集成浅信息和深层信息。

本文将交叉熵损失引入了注意力模块，并将欧几里得损失用于人群计数。标准损失函数将导致模型训练偏向于估计密度。为了应对由不平衡密度水平引起的估计误差，我们提出了自适应密度水平损失(ADLoss)。ADLoss可以自适应地将密度图划分为三级子图。

综上所述，本文有以下贡献：
(1) 我们设计了一个由上下文引导的模块，它连接了多尺度的上下文特征，以提供丰富的上下文信息密集的注意力扩展块(DADB)。
(2）除了一般的欧几里得损失外，我们还引入了交叉熵损失和自适应 密度能级损失(ADLoss)。
(3) 该结果在五个具有挑战性的人群计数数据集(ShanghaiTech(Part_A和Part_B)、WorldEXPO'10，UCSD，UCF_CC_50)上进行了广泛的测试，该方法始终优于其他优秀的方法。

## 实验结果总结
我们在ShanghaiTech(Part_A和Part_B)数据集、UCF_CC_50数据集、UCSD数据集和 WorldExpo’10数据集上评估我们的模型。
图3-1显示了注意力的产生映射在所有这五个数据集。 然后，我们进行了消融研究，以分析在ShanghaiTech Part_B 数据集上提出的CDADNet的配置。如表1所示，密集扩展块(DDB)模块和上下文引导模块显著提高了性能。

![3-1](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/3.1.png)

![table1](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/table1.png)

表2显示密集注意力膨胀模块(DADB)获得比DDB获得更好的性能。

![table2](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/table2.png)

使用不同数量的DADB可以在不同的密度图上实现不同的性能，如图所示3-2

![3-2](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/3.2.png)

此外，为了验证ADLoss的有效性，我们分别测试了两层、三级和四级ADLoss。实验结果见表3，结果表明，ADLoss进一步提高了CDADNet的计数性能。

![table3](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/Table3.png)

此外，统计分析清楚地表明，我们的方法降低了多个密度水平区域的预测损失。试验结果如图3-3所示。

![3-3](https://github.com/NjtechCVLab/Level_2/blob/main/Crowd_Counting/Signal_processing_image_communicaiton/imgs/3.3.png)

结果表明，我们的方法已经取得了出色的性能。因此，我们可以得出结论，该方法具有超优异的通行能力。
