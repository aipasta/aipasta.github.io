---
layout: post
mathjax: true
title: Probability and Statistics
tags: [Basic concept, statistics]
excerpt_separator: <!--more-->
---

This post is about basic concepts of probability and statistics.
<!--more-->

## Questions

- What is random variable?
	- Random variable is a mapping from event to the real number. 
	- A random variable is a measurable function $ X\colon \Omega \to E$ from a set of possible outcomes $\Omega$  to a measurable space $E$. [wiki](https://en.wikipedia.org/wiki/Random_variable)
- What is the meaning of independent random variable?
	- Two random variables are independent if the realization of one does not affect the probability distribution of the other. [wiki](https://en.wikipedia.org/wiki/Independence_(probability_theory))
	-  for every $x$ and $y$, the events $\{X\leq x\}$ and $\{Y\leq y\}$ are independent events
	- Another explanation [link](https://www.statisticshowto.datasciencecentral.com/independent-random-variables/)
		- An independent random variable is a random variable that doesn’t have an effect on the other random variables in your experiment. 
		- Independent events are defined as meeting the following condition: $P(x\|y) = P(x)$, for all values of $X$ and $Y$.
		- Independent random variables that are also discrete variables can be described in a similar way: $P(X = x, Y = y) = P(X = x) P(Y = y)$, for all values of $x$ and $y$.
- What is covariance?
	- Covariance is a measure of the joint variability of two random variables [wiki](https://ko.wikipedia.org/wiki/공분산)
	- $Cov(X, Y)=E[(X-\mu X)(Y-\mu y)]$
- Covariance matrix
	- Every covariance matrix is positive semi-definite. [wiki](https://en.wikipedia.org/wiki/Covariance_matrix#Which_matrices_are_covariance_matrices?)
	- Every covariance matrix is symmetric
- What is positive definite matrix?
	- In linear algebra, a **symmetric** $n\times n$ real matrix $M$ is said to be positive definite if the scalar $ z^{\textsf {T}}Mz$ is **strictly positive** for every non-zero column vector $z$ of $n$ real numbers.
- Law of large numbers
- Central limit theorem
	- 동일한 확률 분포를 가진 확률변수 $n$개의 평균의 분포는 $n$이 충분히 크다면 정규분포에 가까워 진다.
	- The **central limit theorem** states that if you have a population with mean μ and standard deviation $\sigma$ and take sufficiently large random samples from the population with replacementtext annotation indicator, then the distribution of the sample means will be approximately normally distributed. 
	- The sample mean will be approximately normally distributed for large sample sizes, regardless of the distribution from which we are sampling
	- Lindeberg–Lévy central limit theorem
		- 독립 확률 변수 
		- $/mu$ 와 $/sigma$ 가 유한
		- 같은 분포를 가짐 
		
그냥 내가 궁금해진거

- What is the Odd Ration? 조금 더 봐야함 [link](https://www.statisticshowto.datasciencecentral.com/odds-ratio/)
	- An odds ratio (OR) is a measure of association between a certain property A and a second property B in a population. 
	- Specifically, it tells you how the presence or absence of property A has an effect on the presence or absence of property B
	

Reference 

- [Basic definition about statitics](https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/probability-main-index/)