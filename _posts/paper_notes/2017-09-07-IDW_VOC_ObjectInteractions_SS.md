---
layout: post
category: paper_notes
title:  Learning Object Interactions and Descriptions for Semantic Image Segmentation
date: 2017-09-07
---
## Segmentation
###  Learning Object Interactions and Descriptions for Semantic Image Segmentation

This work significantly increases segmentation accuracy of CNNs by learning from an Image Descriptions in the Wild (IDW) dataset

Specifically, useful object interactions or relationships can be extracted from IDW, such as 'girl holding sheep' and ‘girl playing with sheep’, which are not encoded in the per-pixel labelmaps of VOC12.

Accuracies of image segmentation and prediction of object interactions in both VOC12 and IDW are significantly increased

#### Contributions
- This is the first attempt to show that image descriptions in the wild without manually cleaning and refinement are able to improve image segmentation
- IDW-CNN is proposed to jointly learn from VOC12 and IDW.
- IDW-CNN is capable of constantly improving segmentation accuracy

![](/assets/paper_notes/IDW_VOC_ObjectInteractions_SS/image1.png)
Fig.1 (a) provides an example with ‘human’ and ‘sheep’ as keywords.An image of ‘human’ and ‘sheep’ in VOC12 and its annotation are given in Fig.1 (b).

![](/assets/paper_notes/IDW_VOC_ObjectInteractions_SS/table1.png)
Supervision of some works are compared in Table 1, including per-pixel annotation, image-level annotation, bounding boxes (bbox), scribble, and language.

![](/assets/paper_notes/IDW_VOC_ObjectInteractions_SS/image2.png)
Some statics about each object category in VOC12 and image distribution of these objects.

**Image Description Representation:**
- use the Stanford Parser to parse image descriptions and produce constituency trees
- convert constituency trees into semantic trees, which only contains objects and their interactions,these steps are shown in Fig.3. 
	1) First filter the leaf nodes by their part-of-speech, preserving only nouns as object candidates, and verbs and prepositions as action candidates
	2) Nouns are converted to objects and use the lexical relation data inWordNet [19] to unify the synonyms
	3) Verbs should also be recognized and refined and map the verbs to the defined 21 actions using word2vec


#### Learning Image Descriptions
**Data Collection**
- 21 prepositions and verbs that are frequently presented，20 object categories from VOC12，‘subject + verb/prep. + object’ leads to 20×21×20 = 8400
different phrases.
- discard the invalid phrases, such as ‘person ride cow’, if the number of their retrieved images is smaller than 150

**Image Description Representation**	
- Each image description is automatically turned into a parse tree, where select useful objects (e.g. nouns) and actions (e.g. verbs) as supervisions during training

The conversion process generally involves three steps(shown in Fig.3),given a constituency tree:
- 1)first filter the leaf nodes by their part-of-speech, preserving only nouns as object candidates, and verbs and prepositions as action candidates
- 2)nouns are converted to objects,use the lexical relation data in WordNet to unify the synonyms
- 3)verbs should also be recognized and refined,map the verbs to the defined 21 actions using word2vec

![](/assets/paper_notes/IDW_VOC_ObjectInteractions_SS/image3.png)

#### Network Overview
The diagram of IDW-CNN are shown in Fig.4
![](/assets/paper_notes/IDW_VOC_ObjectInteractions_SS/image4.png)
**Feature Extraction**
- IDW-CNN employs DeepLab-v2 as a building block for feature extraction

**Seg-stream**
- The above features are employed by a convolutional layer to predict segmentation labelmap.

**Int-stream**
- Examples of $$h_{person}^{m}$$ and $$h_{bike}^{m}$$ in an image are given in Fig.5(a) and (b).

![](/assets/paper_notes/IDW_VOC_ObjectInteractions_SS/image5.png)

This stream has three stages
- reduce the number of feature channels from 2048 to 512 by a convolutional layer,
- each $$h_{i}^{m}$$is utilized as input to train a corresponding object subnet,outputs a probability characterizing whether object i is presented in image
- train 22 action subnets2 as outlined in blue, each of which predicts the action between two appeared objects

**Object-Pair Selection (OPS)**
- OPS is an important component in Int-stream,which merges features of the presented objects

**Refinement**
- Use a vector as a filter to refine the segmentation,element in that vector express object i is appeared in image I

#### Training Approach
IDW-CNN estimates a pseudo label by predict segmentation labelmap(denoted as $${I\widetilde}^s$$)for each sample and treats it as ground truth in BP.

**Backwards of Seg-stream**
- As shown in the first two red arrows of Fig.4(a), seg-stream has two identical softmax loss functions.

**Backwards of Int-stream**
- As illustrated in the third and forth red arrows of Fig.4(a),

**Implementation Details**
- all losses are deactivated except the first one as marked by ‘1.’ in red of Fig.4(a).
- three losses except the fourth one are optimized by using VOC training set to improve segmentation.
- parameters are jointly fine-tuned by all loss functions to transfer knowledge between VOC and IDW.

**End!**
