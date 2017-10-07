---
layout: post
category: paper_notes
title: Deep Dual Learning for Semantic Image Segmentation 
date: 2017-08-14
---
# Semantic Segmentation

## Deep Dual Learning for Semantic Image Segmentation[[Paper]](http://personal.ie.cuhk.edu.hk/~pluo/pdf/luoWLWiccv17.pdf)

This paper proposed a system named Dual Image Segmentation(DIS) to solve semantic segmentation tasks,which utilize training samples of per-pixel labelmaps and some training samples of image-level tags,and get preferable results.

Definition:
- I:input image
- L:ground-truth labelmap of pixel mark
- T:image tags
- w:weak-mark just image label
- f:full-mark,pixel level label

$$I^w$$ represents a weakly labeled image that only has tags $$T^w$$, but its labelmap $$L^w$$ is missing.An image that is fully annotated with both labelmap $$L^f$$ and tags $$T^f$$

- Given an image with tags only, its labelmap can be inferred by leveraging the images and tags as constraints
- DIS is able to clean tags that have noises.
- DIS significantly reduces the number of perpixel annotations in training, while still achieves state-of-the-art performance

![](/assets/paper_notes/DDualLearing_SS/image1.png)
