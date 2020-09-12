---
layout: post
mathjax: true
title: Logistic Regression
tags: [Basic concept, ML]
excerpt_separator: <!--more-->
---


이름 그대로 Logistic 함수를 이용한 regression. 일반적으로 categorical data 라고 불리는 데이터들에서 classification 문제를 해결하기 위해 주로 사용된다.
이 logistic regression에 사람들이 관심을 갖는 이유는 Neural network 로 가는 과정에 있는 친구이기 때문인가?

<!--more-->


그럼 왜 logistic 함수를 이용하는 것인가? sigmoid function 이라고도 불리는 이 함수는 (둘의 관계가 정확히 어떻게 됨? 같은건가?)  $(-\infty, \infty) \rightarrow (0, 1)$  로 mapping 되는 함수이다. 따라서 output으로 0 에서 1 사이의 어떤 값을 가지는 함수를 fitting 하기에 적절하다고 할 수 있다. 대표적인 예로 확률과 같은 값을 fitting 할 수 있을것 같다. 그리고 2개의 class 있는 classificiation 문제에도 적용 될 수 있다. 하나의 class를 0 나머지 하나를 1 이라고 두고 fitting을 함으로써 가능하다.

logistic regression 에 대해 다음과 같은 두 가지 방법으로 사람들이 해석을 주로 한다.


#### 해석 1. 

0 또는 1에 분포하는 데이터를 fitting 하기 위하여 sigmoid 함수 (logistic 함수; $h(x)$)를 활용하여 피팅함. 그때 나오는 $h(x)$ 값은 특정 라벨을 가질 확률 이라고 해석할 수 있음. 조금 더 정확히 쓰면,

$h_\theta(x)=g(\theta^T x)$, where $g(z)=\frac{1}{1+e^{-z}}$.

하고 싶은건 위의 식에서 주어진 데이터에 대하여 loss 를 minimize 하는 $\theta$를 찾는 거임.

loss 에 대한 설명은 아마도 조금 뒤에서...

#### 해석 2. 

기본적으로 linear 함수를 이용한 regression 이 간단하지만 잘 동작한다.
However, when the data is categorical it is difficult to apply linear regression model.

Suppose that $y$ is a realvalue $\in [0,1]$.
Basically, the regression is to find a function $f$ which fits $f(x)$ to $y$. 
Instead, what about doing the regression to the value which is mapped from y throug function $g$.

That is, we will find another function $h$ which fits $h(x)$ to $g(y)$. 

$g$ 라는 함수를 아래와 같이 두자

$g(y)=\log\left(\frac{y}{1-y}\right)$

Thus, we will fiting $g$ with linear function.

$g(y)=\theta^T x $

$y=\frac{1}{1+e^{-\theta^T x}}$

What is Logistic Function?

- Logistic function (sigmoid function): $y=\frac{1}{1+e^{-x}}$
- Odds: $\frac{P(A)}{P(A^c)}=\frac{P(A)}{1-P(A)}$

근데 갑자기 왜 p 에 관심을 갖는거지?
이제까지 linear regression 같은건 y값 자체를 관심을 가지고 loss도 y 값을 기준으로 만들었는데, 여기서 그럼 loss 는 어떻게 정의 되는거지?

문제를 쉽게 만들기 위해서?
(그럼 문제를 바꿔서 풀어봅시다. 회귀식의 장점은 그대로 유지하되 종속변수 Y를 범주가 아니라 (범주1이 될)확률로 두고 식을 세워 보자는 것입니다. 우변은 그대로 두고 좌변만 확률로 바꾸면 다음과 같습니다.)

그냥 sigmoid로 fitting 한거고, 해석하자면 확률로 볼 수 있음

objective function 이 따로 있음

크로스 엔트로피
두 확률 분포의 차이를 measure 하는 metric 으로 사용 됨 [wiki (cross entropy)](https://en.wikipedia.org/wiki/Cross_entropy#Cross-entropy_error_function_and_logistic_regression)
![Objective](https://i.stack.imgur.com/XbU4S.png)


Reference 

- [blog](https://ratsgo.github.io/machine%20learning/2017/04/02/logistic/)
- Derive cost function [cost function](https://stats.stackexchange.com/questions/278771/how-is-the-cost-function-from-logistic-regression-derivated)
- 로스에 대한 그림 표현 [link](https://towardsdatascience.com/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a)

