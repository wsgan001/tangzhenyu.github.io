---
layout: post
category: paper_notes
title: Understanding Convolution for Semantic Segmentation
date: 2017-09-11
---

# Understanding Convolution for Semantic Segmentation”

Pretrained model:[https://goo.gl/DQMeun](https://goo.gl/DQMeun)

Improve segmentation performance in image encoder network and decoder network by using different two methods.In encoding phase,using densely upsampling convolution(DUC) to generate pixel-wise prediction,DUC can capture lost information in upsampling process by using bilinear interpolation.In encoder phase,using hybrid dilated convolutions to replace standard dilated convolutions,which can solve "gridding" problem.

**Densely upsampling convolution architecture**

The goal of this block is to generate segmentation marked image as same size as original image,resnet-101 that has DUC layer is as follows:

![](/assets/paper_notes/understandingCSS/understandingCSS1.jpg)

The input dimension of DUC is h*w*c,the output dimension of it is h*w*(r^2 * L),through softmax layer,dimen become H * W * L,then getting last feature map through pixel-wise argmax operation.The core idea of DUC is:split marked map into some small blocks that have same size as input feature map.Through r^2 times stack operation,can get global marked map.This make only need convolution operation in upsampling process,without need other parameter.

**Hyybrid Dilated Convolution**

Dilated convolution has gridding problem,it add zero in convolutional kernel,when dilated rate equal 2,about 75 percent information will lose.With dilated rate increasing,local information will lose,long distance span information will lead unrelated and mutual interference.HDC use different dilated rate in different layers,the rate obey distribution like zigzag wave,which make network acquiring multi-scale pixel information.

![](/assets/paper_notes/understandingCSS/understandingCSS2.jpg)

**Experiment Results**

Replace 7*7 concolution kerel layer in ResNet-101 to two 3*3 convolution kernel,get 80.1% mIOU in CityScapes Dataset.

![](/assets/paper_notes/understandingCSS/understandingCSS3.jpg)

**End!**
