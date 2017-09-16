---
layout: post
category: paper_notes
title: Effective Use of Dilated Convolutions for Segmenting Small Object Instances 
date: 2017-08-14
---
## Semantic Segmentation

### Effective Use of Dilated Convolutions for Segmenting Small Object Instances [[Paper]](http://personal.ie.cuhk.edu.hk/~pluo/pdf/luoWLWiccv17.pdf)

This paper proposed a system named Dual Image Segmentation(DIS) to solve semantic segmentation tasks,which utilize training samples of per-pixel labelmaps and some training samples of image-level tags,and get preferable results.

![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image1.png)

**Feature of the satellite imagery:**

- The size of objects is small
- The layout of objects is 

**Differences between satellite imagery and ground-based image**

- (i) Size of objects: compared to the ground-based image, the objects in the satellite imagery are significantly smaller1. 
- (ii) Layout of objects: in satellite imagery, the objects are densely located. In light of these differences, designing a dedicated architecture is obviously needed for remote-sensing segmentation rather than directly employing modern CNN architectures

To segment such a tight crowd of small objects, one of the most important elements is context in an image. [26] showed the importance of context for CNNs to recognize small objects.

**Importance of context for CNNs to recognize small objects**

- Although subsampling layers are helpful to expand the receptive field, they ignore the other important element: resolution.
- The resulting coarse features can miss the details of small objects that are difficult to recover even with efforts such as skip connections [1, 5] or hypercolumns

**Dilated convolutions**

- expand the receptive field without losing resolutions.
- the alignment of the kernel weights is expanded by dilation factor.
- by monotonously increasing the dilation factors through layers, the receptive field can be effectively expanded without loss of resolution

Aggressively increasing dilation factors fails to aggregate local features of small objects. This means that whereas increasing dilation factors is important in terms of resolution and context, it can be detrimental to small objects. This is especially undesirable for remote sensing scenario.
Solve this problem by simply going against the tide—decreasingly dilated convolutions.

Overview of the proposed network architecture 

![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image2.png)

Schematic of the proposed segmentation model:
-front-end module, local feature extraction (LFE) module and head module 

- front-end module is designed to extract features that cover large context,
- LFE module is dedicated to aggregating local features scattered by the front-end module
- the head module outputs a probability map with the same resolution as input

**LFE module**

![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image3.png)

Problem:
- local structure cannot be extracted in higher layer,spatial consistency between neighboring units becomes weak
- local features are aggregated as the kernel weights get denser through the LFE module

Problem on spatial inconsistency：
- We can see that information pyramids of two adjacent units do not overlap due to the sparse connections of the dilated kernels 
- In the case of the dilation factor of 2, two neighboring units have non-overlap information pyramids, and as we increase the dilation factor, number of
neighboring units which have non-overlap information pyramids grows larger. 
- this causes spatial inconsistency between neighboring units and causes serious jaggy patterns in final output maps

Problem on local structure extraction: 
- information pyramids do not overlap for two adjacent units in bottom most layer. All units in top most layer receive information from either of the two units, but not both. This means that all units in top most layer are unaware of local structure inside the two units.


Solutions:

First increasing dilation factor，then decreasing dilation factor
- attach structure with decreasing dilation factor after increasing one, information pyramids of neighboring units can be connected again
- decreasing structure gradually recovers consistency between neighboring units and extracts local structure in higher layer

Post-processing:
- mask proposals for individual object instances are acquired by simply thresholding the output probability map.

#### Experiments
$$Toyota City Dataset:**
![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image4.png)

**Relative improvements:**
![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image5.png)

**Output probability maps for different models:**
![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image6.png)

**Result of Massachusetts Buildings Dataset:**
![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image7.png)

**Result of Vaihingen Dataset:**
![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image8.png)

**output probability maps for different resolution of Massachusetts Buildings Dataset:**
![](/assets/paper_notes/DilatedCNNSegmentingSmallObjectInstances/image9.png)

[26] P. Hu and D. Ramanan. Finding Tiny Faces. arXiv preprint arXiv:1612.04402, 2016.
[27] W. Luo, Y. Li, R. Urtasun, and R. Zemel. Understanding the Effective Receptive Field in Deep Convolutional Neural Networks. NIPS, 2016.