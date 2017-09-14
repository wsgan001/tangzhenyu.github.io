---
layout: post
category: paper_notes
title: ACL 2017 paper reading
date: 2017-06-08
---

# Papers
- [Multimodal Word Distributions](https://arxiv.org/abs/1704.08424)
- [Topically Driven Neural Language Model](https://arxiv.org/abs/1704.08012)
- [Towards End-to-End Reinforcement Learning of Dialogue Agents for Information Access](https://arxiv.org/abs/1609.00777)
- [Learning to Skim Text](https://arxiv.org/abs/1704.06877)
- [From Language to Programs: Bridging Reinforcement Learning and Maximum Marginal Likelihood](https://arxiv.org/abs/1704.07926)

***

## Multimodal Word Distributions

The core idea of this paper is to use Gaussian Mixture Model to express every word embedding,which are different from past idea that learning word embedding for every word.

In ICLR 2015,in paper "Word Representations via Gaussian Embedding",Luke Vilnis and Andrew McCallum from UMass proposed using distribution to express a word embedding.Specifically,they think this embedding is expectation of a gaussian distribution,get a embedding distribution through learning parameter of the gaussian distribution(expectation and variance).This extend the idea of word embedding.But,the drawback of this idea is obvious,using a distribution to express a word cannot demonstrate multiple meanings of this word,and it brings this paper.

This paper want to use Gaussian Mixture Model to learn word embedding.That means,every word embedding is a mixture of multiple gaussian distrition,instead of expectation of a gaussian distribution,which brings a approach to model multiple meanings of word.Defining a objective function,named Max-margin Ranking Objective,and take Expected Likelihood kernal to measure similarity of two distribution

![](/assets/paper_notes/acl2017/image1.jpg)

***

## Topically Driven Neural Language Model 

![](/assets/paper_notes/acl2017/image2.jpg)

***

## Towards End-to-End Reinforcement Learning of Dialogue Agents for Information Access

***

## Learning to Skim Text

![](/assets/paper_notes/acl2017/image3.jpg)

***

## From Language to Programs: Bridging Reinforcement Learning and Maximum Marginal Likelihood

***

**End!**
