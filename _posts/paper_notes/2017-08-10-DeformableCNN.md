---
layout: post
category: paper_notes
title: Deformable Convolutional Networks
date: 2017-08-10
---

# Deformable Convolutional Networks [[Paper]](https://arxiv.org/pdf/1703.06211.pdf)

This paper introduce two new modules to enhance the transformation modeling capability of CNNs, namely, deformable convolution and deformable RoI pooling. Both are based on the idea of augmenting the spatial sampling locations in the modules with additional offsets and learning the offsets from the target tasks, without additional supervision.

This approach shares similar high level spirit with spatial transform networks and deformable part models. They all have internal transformation parameters and learn such parameters purely from data

**Two ways to accomodate geometric variations or model geometric transformations in object scale, pose, viewpoint, and part deformation.**
- build the training datasets with sufficient desired variations,robust representation can be learned from the date.
- use transformation-invariant features and algorithms,like SIFT(use transformation-invariant features and algorithms) and sliding window based object detection paradigm.

**Two drawbacks:**
- the geometric transformations are assumed fixed and known,prevents generalization to new tasks possessing unknown geometric transformations.
- handcrafted design of invariant features and algorithms could be difficult or infeasible for overly complex transformations,even when they are known.

The capability of CNN for modeling geometric transformations mostly comes from the extensive data augmentation, the large model capacity, and some simple hand-crafted modules.
- adaptive determination of scales or receptive field sizes is desirable for visual recognition with fine localization.


**Deformable Convolution**
- sampling using a regular grid R over the input feature map x; 2) summation of sampled values weighted by w.
- It adds 2D offsets to the regular grid sampling locations in the standard convolution. It enables free form deformation of the sampling grid. 

![](/assets/paper_notes/DeformableCNN/image1.jpg)

The offsets are learned from the preceding feature maps, via additional convolutional layers.The deformation is conditioned on the input features in a local, dense, and adaptive manner.

![](/assets/paper_notes/DeformableCNN/image2.jpg)

Above figure showing that deformable convolution generalizes various transformations for for scale,(anisotropic) aspect ratio and rotation.

Normal convolution operation:

![](/assets/paper_notes/DeformableCNN/image3.jpg)

Deformable convolution operation:

![](/assets/paper_notes/DeformableCNN/image4.jpg)

The comparation between normal convolution and deformable convolution:

![](/assets/paper_notes/DeformableCNN/image5.jpg)

![](/assets/paper_notes/DeformableCNN/image6.jpg)

** Deformable RoI Pooling**
- RoI pooling is used in all region proposal based object detection methods.It converts an input rectangular region of arbitrary size into fixed size features
- It adds an offset to each bin position in the regular bin partition of the previous RoI pooling.

The definition of pooling operation:

![](/assets/paper_notes/DeformableCNN/image7.jpg)

The definition of deformable pooling operation:

![](/assets/paper_notes/DeformableCNN/image8.jpg)

This offsets can learn from a full convolutional layer.

![](/assets/paper_notes/DeformableCNN/image9.jpg)

![](/assets/paper_notes/DeformableCNN/image10.jpg)

**Experiments Result:**

**End!**
