---
layout: post
mathjax: true
title: Machine Learning Basic
tags: [Basic concept, ML]
excerpt_separator: <!--more-->
---

Basic conceps about machine learning

<!--more-->

**KL-Divergence**

- Entropy
	- It can be interpreted as the minimum average length of message when we encode p(x)
- Cross entropy
	- Average length of message from p(x) using code for q(x) 
- KL-Divergence: [link](https://www.opentutorials.org/module/3653/22932)
	- Cross entropy(P\|Q) - entropy(P)
	- If Q is equal to P, then it will be minimized
- Mutual information
	- How much mutual dependent two random variable are
	- $I(x,y)=KL(p(x,y)\|\|p(x)p(y))$
	
Newton method

- 폐구간 $[a,b]$에서 실수$R$ 에 대하여 정의된 $f:[a,b]\rightarrow R$ 이 미분가능할 때 방정식 $f(x) = 0$ 의 해를 근사적으로 찾을 때 유용하게 사용되는 방법
- 방법 요약
	- 과정 1) 임의의 x 를 정한다.
	- 과정 2) f(x)값이'0' 인지 확인한다.0이라고 해도 될 정도로 작은 값이면 종료, 0이라고 할 수 없는 값이면 3)으로 진행  
	- 과정 3) f(x)의 접선을 그린다.
	- 과정 4) 접선과 x축이 만나는 지점으로 x를 옮긴다.
	- 과정 2)에서 4)반복을 통해 f(x) = 0 인 지점을 찾는다.

Optimizer

![optimizer: 출처: 하용호, 자습해도 모르겠던 딥러닝, 머리속에 인스톨 시켜드립니다](https://image.slidesharecdn.com/random-170910154045/95/-49-638.jpg?cb=1505089848)

- Gradient descent
- SGD: 모든 자료를 검토하는 게 아니라 조금만 보고 결정을 내림
- RMSProp: multi dimension 의 데이터의 경우 step size를 dim에 따라 이전에 얼마나 바꿔봤는지에 따라 다르게 줌
- Momentum: x 업데이트 할 때, 이전 변화방향을 고려해서 함
- Adam: 위의 두 방법 합침
- 설명 [link](https://sacko.tistory.com/42)
- 설명2 [link](http://shuuki4.github.io/deep%20learning/2016/05/20/Gradient-Descent-Algorithm-Overview.html)


