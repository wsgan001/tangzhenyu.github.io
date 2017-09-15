---
layout: post
category: paper_notes
title: DeepLab Series for Semantic Segmentation
date: 2017-08-11
---
***

## DeepLab v1-Semantic Image Segmentation with Deep Convolutional Nets and Fully Connected CRFs


***

## DeepLab v2-Semantic Image Segmentation with Deep Convolutional Nets, Atrous Convolution,and Fully Connected CRFs


***

## DeepLab v3-Rethinking Atrous Convolution for Semantic Image Segmentation

**Factor1**
- Problem:the reduced feature resolution caused by consecutive pooling operations or convolution striding, which allows DCNNs to learn increasingly abstract feature representations
- Solution:Atrous solution:allows us to repurpose ImageNet pretrained networks to extract denser feature maps by removing the downsampling operations from the last few layers and upsampling the corresponding filter kernels

**Factor2**
- Problem:Existence prblems of objects at multiple scales
- Solution1:DCNN is applied to an image pyramid to extract features for each scale input,where objects at different scales become prominent at different feature maps
- Solution2:the encoder-decoder structure exploits multi-scale features from the encoder part and recovers the spatial resolution from the decoder part
- Solution3:extra modules are cascaded on top of the original network for capturing long range informatio,like DenseCRF or other extra convolutional layers in cascade.
- Solution4:spatial pyramid pooling probes an incoming feature map with filters or pooling operations at multiple rates and multiple effective field-of-views,like PSPNet.


![](/assets/paper_notes/deeplabv3/image1.jpg)

Proposed four types of Fully Convolutional Networks (FCNs) to exploit context information for semantic segmentation,which allows us to effectively enlarge the field of view of filters to  incorporate multi-scale context,in the framework of both cascaded modules and spatial pyramid pooling.See Fig.2 for illustration.

![](/assets/paper_notes/deeplabv3/image2.jpg)

**Method**

- Atrous convolution is applied to extract dense features for semantic segmentation.Standard convolution is a special case for rate r = 1, and atrous convolution allows us to adaptively modify filter’s field-ofview by changing the rate value. See Fig.1 for illustration

- Cascaded Fig.3 and Parallel architecture Fig.4.

Following is cascaded module,block1 to block4 is resnet block,block 5 to block 7 is the replicate of block 4,every block contain three convolutional layers.

![](/assets/paper_notes/deeplabv3/image3.jpg)

Following is parallel module architecture,the main difference from the ASPP of deeplab v2 is that it using global average pooling(enlighten from PSPNet) and add batch normalization layer to help training.

![](/assets/paper_notes/deeplabv3/image4.jpg)

- Multigrid:employ a hierarchy of grids of different sizes and adopt different atrous rates within block4 to block7 in the proposed model.It was Hybrid Dilated Convolution (HDC) originate from [Understanding Convolution for Semantic Segmentation](http://arxiv.org/pdf/1702.08502.pdf).Before,add atrous rate in every resnet block,if the rate of all continuous convolution layer are the same,it cause gridding problem,so it seems like the field of view is enlarged,but only sparse information can be used.

**Experiment Results**

![](/assets/paper_notes/deeplabv3/image5.jpg)

The DeepLabV3-JFT method is employing the ResNet-101 model which has been pretraind on both ImageNet and the JFT-300M dataset

***
