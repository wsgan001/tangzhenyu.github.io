---
layout: post
category: paper_notes
title: Effective Use of Dilated Convolutions for Segmenting Small Object Instances in Remote Sensing Imagery
date: 2017-09-15
---
# Semantic Segmentation

##Effective Use of Dilated Convolutions for Segmenting Small Object Instances in Remote Sensing Imagery[[Paper]](https://arxiv.org/abs/1709.00179)

Objects in remote sensing imagery are small and crowded.This paper proposed a novel architecture called local feature extraction(LFE) module to tackle these problems,the module attached on top of dilated front-end module.

**Factor:**
- Problem:Aaggressively increasing dilation factors fails to aggregate local features due to sparsity of the kernel, and detrimental to small objects.
- Solution:aggregating local features with decreasing dilation factor.

**Difference between satellite imagery and ground-based image**
- Size of objects: compared to the ground-based image, the objects in the satellite imagery are significantly smaller1
- Layout of objects: in satellite imagery, the objects are densely located. In light of these differences, designing a dedicated architecture is obviously needed for remote-sensing segmentation rather than directly employing modern CNN architectures



![](/assets/paper_notes/DilatedCNNSegSmallObjectRSI/image1.jpg)
