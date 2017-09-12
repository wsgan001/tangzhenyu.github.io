---
layout: post
category: paper_notes
title: Papers about instance segmentation by MSRA
date: 2017-06-08
---

# Instance Segmentation+MSRA

**Paper Link:[Instace-sensitive Fully Convolutional Networks.ECCV 2016](https://arxiv.org/abs/1603.08678)**
**Paper Link:[R-FCN:Object Detection via Region-based Fully Convolutional Networks]()**
**Paper Link:[Fully Convolutional Instance-aware Semantic Segmentation]()**

# InstaceFCN[Instace-sensitive Fully Convolutional Networks.ECCV 2016]

This paper propose a method to extract mask proposal.The mask proposal here is similar as the proposal in Faster R-CNN.

Propose instance-sensitive score map,which encode relative position information in feature map.Actually,it means different feature map more suitable for process different region,and put this sub-region together to get last feature map.

**1.Network architecture**

![](/assets/paper_notes/instanceSegMSRA/image1.jpg)

**End!**
