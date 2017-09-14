---
layout: post
category: paper_notes
title: Papers about instance segmentation by MSRA
date: 2017-06-08
---

# Instance Segmentation+MSRA

- [1]Instace-sensitive Fully Convolutional Networks.ECCV 2016[[Paper]](https://arxiv.org/abs/1603.08678)
- [2]R-FCN:Object Detection via Region-based Fully Convolutional Networks[[Paper]](https://arxiv.org/abs/1605.06409)
- [3]Instance-aware semantic segmentation via multi-task network cascades[[Paper]](https://arxiv.org/abs/1512.04412)
- [4]Fully Convolutional Instance-aware Semantic Segmentation[[Paper]](https://arxiv.org/abs/1611.07709)

***

## InstaceFCN[Instace-sensitive Fully Convolutional Networks.ECCV 2016]

This paper propose a method to extract mask proposal.The mask proposal here is similar as the proposal in Faster R-CNN.

Propose instance-sensitive score map,which encode relative position information in feature map.Actually,it means different feature map more suitable for process different region,and put this sub-region together to get last feature map.

**1.Network architecture**

![](/assets/paper_notes/instanceSegMSRA/image1.jpg)

**From FCNs to InstanceFCN**
When consider an image that contains two object instances that are close to each other.Instance-sensitive score maps can be used to discriminate “right side” from “left side”.

**2.Instance-sensitive score maps**

- Relative positions:relative positions are with respect to object instances, such as the “right side” of an object or the “left side” of an object.
- Each output pixel is a classifier of relative positions of instances.

**3.Instance assembling module**

Simply assemble instances from these instance-sensitive score maps.
In Fig.1,k equal 2,windows solution is m*m,the $k^2$ sub-windows are then put together (according to their relative positions) to assemble a new window of resolution m×m. 

**4.Local Coherence**

Local coherence we mean that for a pixel in a natural image, its prediction is mostlikely the same when evaluated in two neighboring windows.e.g two neighboring windows in Fig.3 bottom.

In contrast to DeepMask’s [8] mechanism which is based on a "sliding fc layer".In the case of Fig.3 top,the same pixel in the image coordinate system is predicted by two different channels of the fc layer.The prediction of this pixel is in general not the same when evaluated in two neighboring windows.

Advantages compare to DeepMask:This not only reduces the computational cost of the mask prediction layers, but more importantly, reduces the number of parameters required for mask regression,

***

## R-FCN:Object Detection via Region-based Fully Convolutional Networks

***

## Instance-aware semantic segmentation via multi-task network cascades

***

## Fully Convolutional Instance-aware Semantic Segmentation

This paper is the first one to do end-to-end instance-aware semantic segmentation.

**1.To achieve certain translation-variant property**
- An FCN is applied on the whole image to generate intermediate and shared feature maps;
- From the shared feature maps, a pooling layer warps each region of interest (ROI) into fixed-size per-ROI feature maps
- One or more fully-connected (fc) layer(s) in the last network convert the per-ROI feature maps to per-ROI masks

**2.Above method have drawbacks**
- The ROI pooling step losses spatial details due to feature warping and resizing
- The fc layers over-parametrize the task, without using regularization of local weight sharing.
- The per-ROI network computation in the last step is not shared among ROIs,it is therefore slow for a large number of ROIs.

For [3],the approach takes 1:4 seconds per image, where more than 80% of the time is spent on the last per-ROI step.

For [1],The object segmentation and detection sub-tasks are separated and the solution is not end-to-end.

**3.Method in this paper have some advantages:**
- The underlying convolutional representation and the score maps are fully shared for the object segmentation and detection sub-tasks, via a novel joint formulation with no extra parameters.
- It operates on box proposals instead of sliding windows, enjoying the recent advances in object detection.

**4.Positionsensitive Score Map Parameterization**

**5.Joint Mask Prediction and Classification**

**End!**
