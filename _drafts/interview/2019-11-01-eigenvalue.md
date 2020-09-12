---
layout: post
mathjax: true
title: Eigenvalue and Eigenvector
tags: [Basic concept, CS]
excerpt_separator: <!--more-->
---


# Eigenvalue and Eigenvector

#### 정의

- 행렬 A를 선형변환으로 봤을 때, 선형변환 A에 의한 변환 결과가 자기 자신의 상수배가 되는 0이 아닌 벡터를 고유벡터(eigenvector)라 하고 이 상수배 값을 고유값(eigenvalue)라 한다.

<!--more-->

For $n$ by $n$ matrix $A$, $Av = \lambda v$ 를 만족하는 $v$가 eigenvector, $\lambda$가 eigenvalue 가 된다.


![definition](https://t1.daumcdn.net/cfile/tistory/237AB44F525CD4BC08)

#### 의미

A 를 어떤 선형변환이라고 봤을 때, A라는 선형변환을 하여도 벡터의 방향은 변하지 않고 크기만 바뀌는 vector v 가 존재 할 수 있음. 이때 그 벡터 v를 eigenvector 그리고 바뀐 크기 scale $\lambda$ 를 eigenvalue 라고 할 수 있다.

#### Questions

- What is 대각화?
- 어떻게 구할 수 있음?
- eigendecomposition 이란 무엇인가?
	- 어디에 사용 되는가?
	- 가능한 조건은?
- Symmetric 한건 어떤 영향을 미치는가?
	- SVD 이야기하는 사이트에 나온 요약[link](https://bskyvision.com/251)
	- 요약하면 어떤 행렬을 대각 행렬이 포함된 꼴로 factorization 을 하고싶다. 왜? 대각 행렬끼어 있으면 이런 저런 계산이 편해지나봐 **(이거 확인)** 근데 기존의 eigendecompose 는 $A=S\Lambda S^{-1}$ 이렇게 표현할 수 있는데, A 가 이제 symmetric 하다는 특성이 있으면, $A=Q\Lambda Q^{T}$, 여기서 Q는 orthogonal. orthogonal 하다는 건 transpose 한거가 inverse 라는 거고 그럼 쉽게 inverse 구할 수 있음.