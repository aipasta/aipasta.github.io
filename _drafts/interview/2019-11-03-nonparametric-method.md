---
layout: post
mathjax: true
title: Nonparametric Method
tags: [Basic concept, ML]
excerpt_separator: <!--more-->
---




What is it? One sentence summary

Nonparametric approach is used when no assumption about the data can be made about the input density and the data speaks for itself.

<!--more-->

**Parametric method**

In the parametric approaches,  we assumed that the data is drawn from one or a mixture of probability distributions of known form.
For example, regression with linear function or classification with normal density are based on this assumption.

- The advantage of a parameteric method is that it reduces the problem to extimating the values of a small number of parameters.
- Disadvantage: this assumption does not always hold and it can cause large error


**Parametric estimation**

```All we assume is that similar inputs have similar outputs.```

This assumption is reasonal because the world is smooth and functions change slowly.

**Q** How can we define similar (Is there a metric like a distance?) 

Our algorithm is composed of finding the similar past instances from the training set using a suitable distance measure and interpolating from them to find the right output.

비슷하면 아웃풋도 비슷할 것이다. --> 적당한 distance measure 로 가까운걸 찾고 interpolating.

Different nonparametric method differ in the way they define similarity or interpolate from the similar instances.

It is also called as instance-based or memory based learning, since it stores the training instances in a lookup table and interpolates from these.


<!--more-->

Nonparametric: Similar inputs have similar outputs

 Aka lazy/memory-based/case-based/instance- based learning