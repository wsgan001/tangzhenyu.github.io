---
layout: post
category: paper_notes
title: Black-Box Optimization in Machine Learning with Trust Region Based Derivative Free Algorithm
date: 2017-09-01
---

### Black-Box Optimization in Machine Learning with Trust Region Based Derivative Free Algorithm

![](/assets/paper_notes/DFO-TR/fig1.jpg)

This paper mainly 
- Study the behavior of various black-box methods in a purely continuous setting
- Explore practical scalability of the methods with respect to the dimension of the search space and nonlinearity of the function.
- Apply a variant of a model-based trust region derivative free method, called DFO-TR, (Conn et al.,2009) to directly maximize the AUC function.



**Black-box optimization**
- Bayesian Optimization(BO):BO methods always contain a component that aims at the exploration of the space
- Derivative Free Optimization(DFO):DFO methods are content with a local optimum.DFO methods tend to escape shallow local minima and are quite well suited for problems with a few well defined local basins.
- Random Search:

Using gradient-based optimization to optimize AUC value directly is not feasible,because this funtion is a discontinuous step function,hence its gradients are either zero or undefined.

**Performance comparision between BO and DFO**
- Bayesian optimization methods construct a probabilistic model by using point evaluations of the true function.the subsequent configurations of the parameters will be selected (Brochu et al., 2010) by optimizing an acquisition function which make the per iteration complexity of BO methods increase.
- On the other hand, DFO-TR and other model-based DFO methods content themselves with building a local model of the true function, hence maintenance of such models remains moderate and optimization step on each iteration is cheap.

#### Algorithmic Framework of DFO-TR

DFO-TR framework,as outlined in Algorithm 1.

![](/assets/paper_notes/DFO-TR/alg1.jpg)

Bayesian optimization framework, as outlined in Algorithm 2.

![](/assets/paper_notes/DFO-TR/alg2.png)

For a given linear classifier $$w^{T}x$$, the corresponding AUC value, a (noisy) nonsmooth deterministic function, is obtained as

![](/assets/paper_notes/DFO-TR/equ1.png)

where

![](/assets/paper_notes/DFO-TR/equ1_1.png)

A (probabilistic) model $$M(w)$$ of the true function f computed by using function values computed thus far by the algorithm.

An acquisition function, $$a_M$$, which presents a trade-off between minimizing the model and improving the model, by exploring areas where $$f(w)$$ has not been sampled.

The expected value of AUC is defined as

![](/assets/paper_notes/DFO-TR/equ2.png)

Then $$E[F_{AUC}(w)]$$ is a smooth function of $$w$$.

![](/assets/paper_notes/DFO-TR/theo1.png)

![](/assets/paper_notes/DFO-TR/theo2.png)

![](/assets/paper_notes/DFO-TR/theo3_1.png)
![](/assets/paper_notes/DFO-TR/theo3_2.png)

Then we get the expected value of AUC function,which is a smooth function of $$w$$.

We should note that the assumption of the positive and negative data classes obeying jointly normal distribution is too strong to be satisfied for most of the practical problems.

### Experimens

Compare DFO-TR with SMAC (Hutter et al., 2011), SPEARMINT (Snoek et al., 2012), and TPE (Bergstra et al., 2011), which are popular Bayesian optimization algorithms based on different types of model

#### Optimizing Smooth, NonConvex Benchmark Functions
- Compare the precision $$\Delta f_{opt}$$ with the global optimal value, which is known

![](/assets/paper_notes/DFO-TR/table123.png)

#### Optimizing AUC Function
compare the performance of DFOTR and the three Bayesian optimization algorithms, TPE, SMAC, and SPEARMINT, on the task of optimizing AUC of a linear classifier, defined by w.Table 5 summarizes the results.

![](/assets/paper_notes/DFO-TR/table5.png)

#### Hyperparameter Tuning of Cost-Sensitive RBF-Kernel SVM

Hyperparameter tuning of an RBF kernel, cost-sensitive, SVM, with $$\ell2$$ regularization parameter λ, kernel width γ, and positive class cost $$c_p$$

Compare the performance of DFO-TR random search, and Bayesian optimization algorithms, in tuning a three-dimensional hyperparameter w = (λ, γ, $$c_p$$).The result is outlined in Table 6.

![](/assets/paper_notes/DFO-TR/table6.png)

Figure 2 illustrates the performance of DFO-TR versus random search and Bayesian optimization algorithms, in terms of the average test accuracy over the number of function evluations.

![](/assets/paper_notes/DFO-TR/fig2.png)