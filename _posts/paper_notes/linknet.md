---
layout: post
category: paper_notes
title: LinkNet: Exploiting Encoder Representations for Efficient Semantic Segmentation
date: 2017-09-10
---
# LinkNet: Exploiting Encoder Representations for Efficient Semantic Segmentation

The main features of LinkNet is fast training and running speed both in embedding system TX1 and normal computer gpu TitanX.

Network architecture of LinkNet is as following:

![](/assets/paper_notes/linknet/linknet1.jpg)

conv represent convolution,full-conv represent full-convolution,add BN layer before convolution layer,add Relu layer after this one,left side is encoder process,right side is decoder process,encoder section include residual block ,and linknet use ResNet-18 as encoder,which as follows:

![](/assets/paper_notes/linknet/linknet2.jpg)

The detail of decoder as follows:

![](/assets/paper_notes/linknet/linknet3.jpg)

The contribution of linknet is link every relative layer between encoder and decoder,the input of encoder linking to the output of decoder of parallel depth.

**Experiments Result:**

Efficiency:

![](/assets/paper_notes/linknet/linknet4.jpg)

Performance:

![](/assets/paper_notes/linknet/linknet5.jpg
