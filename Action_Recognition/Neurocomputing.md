# 团队最新研究成果 -- Neurocomputing
+ Aichun Zhu, Qianyu Wu, Ran Cui, Tian Wang, Wenlong Hang, Gang Hua and Hichem Snoussi. "Exploring a rich spatial–temporal dependent relational model for
skeleton-based action recognition by bidirectional LSTM-CNN" in Elsevier ScienceDirect

## 一、前言

随着有效且低成本的人体骨骼捕捉系统的快速发展，基于骨骼的动作识别最近备受关注。大多数现有方法都是使用CNN和LSTM的。近年来，虽然这些方法在基于骨架的动作识别方面取得了良好的性能，但这些方法能力有限，它们仍然面临两大挑战需要解决，一是，骨架数据是对人类行为的高级抽象，大大简化了表示人类行为的困难。这些骨骼关节在一个故咋的树结构钢中成对连接，并导致身体关节的细微变化。在这种情况下，一些没有明显坐标变化的关节能够表示出不同类别的运动。如图1-1所示，它包含了两个微妙的动作：阅读和写字，它们在骨骼信息上很相似区分它们的关键在于手腕和手指的运动信息。第二个挑战是，当转换输入的骨架数据以匹配CNN或LSTM时，会破坏骨架关节之间的空间或时空特征，这就带来了如何有效融合空间和时间特征方面地问题。

![1-1](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/1-1.png)

## 二、本文结构

为解决上述问题，我们提出了一个具有端到端双向LSTM-CNN（BiLSTM-CNN）地时空依赖关系模型。它包含一个时空关系依赖模型和一个双向LSTM-CNN网络。流程图如图2-1所示。

![2-1](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/2-1.png)

人们的身体关节可以直接在图形模型中建立以表示人类的行为，这些行为被描述为一系列明确的动作。骨架动作序列的时空特征由相对位置和相对速度来建模，其中，相对位置可以提供丰富的时空信息，而相对速度具有提供丰富的动态信息的能力。如图2-2所示，人体骨架的树形结构提供了部件之间强有力的空间关系，并且人体动作通常由几个相邻的关节点来完成。因此它们的主要功能是在所提出的依赖关系模型中探索丰富的结构信息。而不同的中i性能关节具有的相邻关节数量也不同，因此需要根据所有相邻关节点来定义中心关节。其中（a）是输入骨架数据，（b）表示中心关节（红色点）和相邻关节（绿色点），（c）表示出了所提出的模型中中心关节和相邻关节的三种组合模式

![2-2](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/2-2.png)

可将整个人体的股价点分为三个不同层次的模型：全局模型、中层模型和局部模型。全局模型从所有的关节中提取详细的关节特征，而中层和局部模型通过肢体关节提供更有效的动作信息。如图2-3所示，所提出的多层次依赖关系模型由三个子模型组成。全局模型由整个人体骨架内的所有关节点构成，中层模型由人体的左半部分和右半部分构成，局部模型由人体四肢的关节构成。

![2-3](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/2-3.png)

通常双分支网络结构利用CNN提取运动的空间信息，利用LSTM提取运动的时间信息，为了更好地融合时空信息进行基于骨架地动作识别，提出了一种端到端地双向LSTM-CNN。双向LSTM主要通过将每个视频序列的向前和向后状态表示为两个独立的隐藏状态，以此捕获过去和未来的状态信息。将关节点的时空依赖模型作为BiLSTM的输入，如图2-4所示。
全局、中层和局部模型的特征分别送入BiLSTM中得到每个动作的丰富上下文信息，3个层次的输出串联在一起作为双向LSTM上的最终输出，并将它作为一个标准CNN网络的输入，该网络用于提取骨架序列的空间信息，并输出人体行为的预测结果。

![2-4](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/2-4.png)

## 实验结果总结
将本文的算法在NTU RGB+D和UTD-MHAD数据集上将每个视频序列的长度设置为100帧，在SBU数据集上设置为35帧，若视频较短，则多次重复最后一帧图像。图3-1给出了关系模型和非关系模型在每个行为类别的识别效果差距，可以看到，于大多数动作类而言，关系模型由于非关系模型，尤其是那些只涉及身体部分的动作类，实验结果表明，我们提出的关系模型能够提高人体动作识别的准确率，捕捉人体动作的细微线索。

![3-1](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/2-4.png)

图3-2表明，多层次模型更能全面地表示动作特征。值得一提的是，由于局部模型将网络的注意力放在了每个关节点上，更能容易捕获关节点细微的变化，因而单独测试时全局模型的识别效果更出色，而所有层次的特征融合在一起时模型既能捕获关节点细微的变化又能掌握关节点整体的变化情况。

![3-2](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/3-2.png)

表3-4表明本算法提出的双向LSTM-CNN模型取得了最高的识别准确率,能够有效地挖掘关节序列中的时空信息。

![3-3](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/3-3.png)

由表3-5、3-6、3-7可知：首先基于深度学习的耳朵行为识别方法在识别效果方面普遍优于使用手工特征的方法（如Lie Group）其次通过对关节点的时空依赖建模，本方法能够获取更加丰富的时空运动特征，使得识别准确率高于目前其他算法。

![3-4](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/3-4.png)

![3-5](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/3-5.png)

![3-6](https://github.com/NjtechCVLab/Level_2/blob/main/Action_Recognition/imgs/3-6.png)

