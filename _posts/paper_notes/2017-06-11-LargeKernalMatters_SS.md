---
layout: post
category: paper_notes
title: Large Kernel Matters-Improve Semantic Segmentation by Global Convolutional Network
date: 2017-06-11
---

### Large Kernel Matters-Improve Semantic Segmentation by Global Convolutional Network
[https://arxiv.org/abs/1703.02719](https://arxiv.org/abs/1703.02719)

The experiment of this paper shown that in the field of semantic segmentation,where we need to perform dense per-pixel prediction,we find that the large kernel (and effective receptive field)plays an important role when we have to perform the classificationand localization tasks simultaneously

This paper proposed Global Convolutional Network to address both the classification and localization issues for the semantic segmentation,and suggest a residual-based boundary refinement to further refine the object
boundaries

####
**Challenges:**
- 1)classification:an object associated to a specific semantic concept should be marked correctly
- 2)localization:the classification label for a pixel must be aligned to the appropriate coordinates in output score map

![](/assets/paper_notes/LargeKernalMatters_SS/Fig1.png)

Current state-of-the-art semantic segmentation models mainly follow the design principles for localization, however, which may be suboptimal for classification

![](/assets/paper_notes/LargeKernalMatters_SS/Fig3.png)

Use large kernal to solve above challanges simultaneously,named "global convolutional network"
**Model Features**
- 1) from the localization view, the model structure should be fully convolutional to retain the localization performance and no fully-connected or global pooling layers should be used as these layers will discard the localization information; 
- 2) from the classification view, large kernel size should be adopted in the network architecture to enable densely connections between feature maps and per-pixel classifiers, which enhances the capability to handle different transformations.

The model architecture shown in Fig.2.

![](/assets/paper_notes/LargeKernalMatters_SS/Fig2.png)

Global Convolutional Network: Instead of directly using larger kernel or global convolution, our GCN module employs a combination of 1 × k + k × 1 and k × 1 + 1 × k convolutions, which enables densely connections within a large k×k region inthe feature map

Boundary Refinement:proposed a Boundary Refinement (BR) block shown in Figure 2 C. Here, we models the boundary alignment as a residual structure.

![](/assets/paper_notes/LargeKernalMatters_SS/fig1.jpg)

Larger kernal size get better performance.

![](/assets/paper_notes/LargeKernalMatters_SS/table1.png)

Compare the model architecture between GCN and other twos.

![](/assets/paper_notes/LargeKernalMatters_SS/Fig4.png)

![](/assets/paper_notes/LargeKernalMatters_SS/table23.png)

![](/assets/paper_notes/LargeKernalMatters_SS/table4.png)

From above table,we can see GCN get better performance than others.

![](/assets/paper_notes/LargeKernalMatters_SS/Fig5.png)

![](/assets/paper_notes/LargeKernalMatters_SS/table6.png)

PASCAL VOC 2012 test set 
![](/assets/paper_notes/LargeKernalMatters_SS/table8.png)

Cityscapes test set 
![](/assets/paper_notes/LargeKernalMatters_SS/table10.png)