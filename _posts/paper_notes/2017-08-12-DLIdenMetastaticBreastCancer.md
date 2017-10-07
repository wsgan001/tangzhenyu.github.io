---
layout: post
category: paper_notes
title: Deep Learning for Identifying Metastatic Breast Cancer
date: 2017-08-12
---

# Deep Learning for Identifying Metastatic Breast Cancer

**Paper Link:<https://people.csail.mit.edu/khosla/papers/arxiv2016_Wang.pdf>**

This paper develop a network architecture for the automated detection of sentinel lymph node biopsies.

Although the pathologist alone is currently superior to our deep learning system alone,combing deep learning with the pathologist produced a major reduction in pathologist error rate,reducing it from over 3 percenet to less than 1 percent.

**Image Pre-processing**

To reduce computation time and to focus analysis on regions of the slide most likely to contain cancer metastasis,we first identify tissue within the WSI and exclude background white space.

![](/assets/paper_notes/DLIMBC/image1.jpg)

**Cancer Metastasis Detection Framework**

The framework consists of a patch-based classification stage and a heatmap-based post-processing stage.

- path-based classification:patch-based classification stage takes as input whole slide images and the ground truth image annotation,indicating the locations of regions of each WSI containing metastatic cancer.

- heatmap-based post-processing:use the tumor probability heatmap to compute the slide-based evaluation and lesion-based evaluation scores for each WSI

The network architecture is as follows:

![](/assets/paper_notes/DLIMBC/image2.jpg)

**Post-processing of tumor heatmaps to compute slide-based and lesion-based probabilities**

- Slide-based Classification:the post-processing takes as input a heatmap for each WSI and produces as out-put a single probability of tumor for the entire WS.Given a whole slide image (Fig. 3 (a)) and a deep learning based patch classification model, we generate the corresponding tumor re-gion heatmap (Fig. 3 (b))

![](/assets/paper_notes/DLIMBC/image4.jpg)

- Lesion-based Detection Post-Processing:identify all cancer lesions within each WSI with few false positives,trained two deep model,model(D-I) using initial training dateset,model(D-II) with a training set that is enriched for tumor-adjacent negative regions.

**Experiments Result**

- Slide-based Evaluation:The merits of the algorithms were assessed fpr descriminating between slides containing metastasis and normal slides.Receiver operating characteristic (ROC) analysis at the slide level were performed and the measure used for comparing the algorithms was area under the ROC curve (AUC).As shown in Fig.4.

![](/assets/paper_notes/DLIMBC/image4.jpg)

- Lesion-based Evaluation:free-response receiver operating characteristic(FROC) curve were used.The FROC curve is defined as the plot of sensitivity versus the average number of false-positives per image.As shown in Fig.5.

![](/assets/paper_notes/DLIMBC/image5.jpg)

**End!**
