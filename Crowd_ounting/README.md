# 经典算法介绍 - CSRNet

## Introduction

It is common to have sizeable crowds in specific events or scenarios(such as video surveillance, traffic control and sport events), and crowd counting from images or videos becomes crucial for applications to public safety. Estimation for crowd counts is via detecting the body or head in early stage. Then, learning a map from local or global handcrafted feature had used in some methods. In recent years, the improvement of accuracy of crowd counting is an serious problem. And the popular solution is density map that values are summed to give the count of crowd within the image. However, it still remains a challenging task for generating accurate crowd density map and performing precise crowd counting for highly congested scenes due to the exit of background noises, occlusions, and non-uniform distribution.  

Recently, researchers have proposed various improved algorithms and models based on deep neural networks(DNN) for generating better density map and have better performance in crowd counting. A number of multi-scale architectures have proposed to handle scale variation on congested scene. They have achieved high performance through multiple networks to integrate information of multiscale features and its performance is restricted by the number of columns or branches. Besides, these architectures containing several columns of CNN or several branches, have two disadvantages when networks go deeper: cost a large amount of training time and produce non-effective branches. A contextual pyramid CNN(CP-CNN) incorporates global and local contextual information to estimate context at various levels for achieving lower count error and better quality density maps. This method takes the spatial distribution of crowd into account through embedding contextual information which is essential for achieving further improvements. An ADCrowNet fuses the visual attention mechanism and deformable convolution scheme. This model achieve impressive result on account of attention mechanism have good performance in handling the occlusion problem and dilated convolutional filters can extract more features. However, there is still a gap between the density map generated by these methods and the ground truth, and there is room for improvement.  

## CSRNet Architecture

![CSRNet Architecture](./imgs/Picture1.png)

## Estimation errors on ShanghaiTech dataset

![Results](./imgs/Picture2.png)

![Samples](./imgs/Picture3.png)
