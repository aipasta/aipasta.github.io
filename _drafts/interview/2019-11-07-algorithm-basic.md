---
layout: post
mathjax: true
title: Algorithm Basic
tags: [Basic concept, CS]
excerpt_separator: <!--more-->
---

This post is about the basic algorithm concepts including reduction, np-hardness.

<!--more-->

## Reduction

- For decision problems X , Y , a reduction from X to Y is:
	- An algorithm...
	- that takes $I_X$, an instance of X as input ...
	- and returns $I_Y$ , an instance of Y as output ...
	- such that the solution (YES/NO) to $I_Y$ is the same as the solution to $I_X$


Comparing with reduction.

- If Problem X reduces to Problem Y (we write X ≤ Y )
	- X is no harder than Y,or Y is at least as hard as X


Polynomial reduction

- Using polynomial-time reductions
	- If X $≤_P$ Y, and we have an efficient algorithm for Y, we have an efficient algorithm for X.
	- If X $≤_P$ Y, and there is no efficient algorithm for X, there is no efficient algorithm for Y .

Example of reduction:

- Independent set ≤ Clique
	- Graph $G$ 가 주어졌을때 $\bar{G}$에서 size $k$인 Clique이 존재하면 $G$ 에서 size $k$ 인 independent set 이 존재함.
	- 즉, clique 문제 풀 수 있으면, independent set 문제 풀 수 있음
	- reduction 완료
	- Clique 문제는 최소 indep set 문제만큼은 어렵다


## Nondeterministic Polynomial Time

**Summary:**

Polynomial Time
- Definition: Polynomial time (denoted by $\bf{P}$) is the class of all (decision) problems that have an algorithm that solves it in polynomial time.

Other concepts:
- Checkability
- Certifiers:
	- (roughly) Algorithm which can 
- Certificate: 예제/proof

Nondeterministic Polynomial Time
- Definition: Nondeterministic Polynomial Time (denoted by $\bf{NP}$) is the class of all problems that have **efficient certifiers**.
- Give certificate가 문제의 정답이 맞는지를 polynomial 시간 안에 대답할 수 있으면 됨. 

Asymmetry in Definition of NP
- 예를 들면, indep set 문제를 생각해봤을때 k 개보다 큰 set 이 있냐는 decision 문제. 여기서 certificate 를 하나라도 찾으면 문제에 yes 라고 대답 가능. 그런데 반다로 안되는 예시를 하나 찾았다고 해서 '존재하냐?'는 문제에 대답을 할 수는 없음.

$\bf{P}$ 와 $\bf{NP}$ 의 관계
- $\bf{P}$집합과 $\bf{NP}$ 집합이 같은지 다른지
- "쉽게 검산할 수 있는 모든 문제들은 모두 쉽게 풀리는가?"


다시 정리 [나무위키](https://namu.wiki/w/P-NP%20%EB%AC%B8%EC%A0%9C)

- 결정문제: 답이 YES 아니면 NO로 반환되는 문제를 결정 문제라고 한다. 예를 들어, 'a는 b의 배수인가?'와 같은 질문은 결정 문제이다. P와 NP 모두 결정 문제의 분류에 해당한다.
- P문제: 
	- 결정 문제들 중에서 쉽게 풀리는 것을 모아 놓은 집합이다. 어떤 결정 문제가 주어졌을 때, 다항식(Polynomial) 시간 이내에 그 문제의 답을 YES와 NO 중의 하나로 계산해낼 수 있는 알고리즘이 존재한다면, 그 문제는 P 문제에 해당된다.
	- 위의 정의는 **결정적 알고리즘(deterministic algorithm)**, 즉 계산의 각 단계에서 단 한가지의 가능성만을 고려할 수 있는 알고리즘이 다항시간이 걸리는 문제가 P문제라는 뜻이다.
- NP문제:
	- NP 문제는 형식적으로는, 문제를 푸는 각 단계에서 여러가지의 가능성을 동시에 고려할 수 있는 비결정적 알고리즘(non-deterministic algorithm)으로 다항시간내에 문제를 해결할 수 있는 문제라고 정의한다. 즉 NP는 Non-deterministic Polynomial의 약자이다. 
	- 검산 위주의 정의: NP 문제는 결정 문제들 중에서 적어도 검산은 쉽게 할 수 있는 것을 모아 놓은 집합으로도 정의할 수 있다.
	- 비 결정론적 튜링머신으로 다항시간 내에 풀 수 있는 문제 [link](https://wkdtjsgur100.github.io/P-NP/)

NP에 대한 다시 정리
- 예 해밀턴 경로 문제; 적절한 모범답안이 주어진 경우 Yes라는 대답은 확인할 수 있다. $\rightarrow$ '해밀턴 경로 문제 = NP 문제'
- 그러나 그 답이 No라면, 설사 '그런 조건을 만족하지 않는 경로'가 주어진다고 하더라도 '그런 경로가 존재하지 않는다'는 것을 확인할 수는 없을 것이다. $\rightarrow$ No라는 답을 다항식 시간 내에 확인할 수 있게 해 주는 종류의 모범답안은 알려져 있지 않다
- 결국 P-NP 문제의 가장 중요한 쟁점은 이 수학적 귀납법으로 경우의 수를 P의 영역으로 넣을 수 있는지의 여부를 묻는 것으로 볼 수 있다. 
- 대표적인 예로, 정렬 문제의 경우 경우의 수가 n!n!이지만, 이미 수학적 귀납법으로 $O(n^2)$, 나아가 $O(n \log n)$으로 수렴된 바 있다.

운에 기대면 현실적인 비용으로 해결할 수 있는(non-deterministic polynomial) 문제들. [다른 링크](https://ratsgo.github.io/data%20structure&algorithm/2017/11/30/NP/)

[turing machine](https://www.youtube.com/watch?v=DDu652WsYbc)
[Nondeterministic turing machine ](https://www.youtube.com/watch?v=gQnPM6sydkk)

Another explanation
- "Nondeterministic polynomial time" is the full definition of NP - "polynomial time" is important - each decision you make might take O(1), but there are polynomially many such decisions, leading to something that can theoretically be solved in polynomial time, if you can make the **right choice at every step** or **execute all options at the same time**. [https://stackoverflow.com/questions/44237335/what-is-nondeterministic-in-np-exactly](https://stackoverflow.com/questions/44237335/what-is-nondeterministic-in-np-exactly)


## NP-hard and NP-complete

- NP hard: 적어도 NP문제 보다는 어려우며, “모든” NP 문제를 다항 시간 내에 어떤 문제 A로 환원(reduction)할 수 있다면, 그 A 문제를 NP-난해(NP-hard) 문제라고 한다. 
	- "모든 NP 문제" $\le_P$ A
- NP-complete: NP-hard에는 두가지 유형이 있다. NP에 속하는 NP-hard문제, NP에 속하지 않는 NP-hard 문제. NP에 속하는 NP-hard문제는 NP-complete 문제임

![np-hard](https://wkdtjsgur100.github.io/images/posts/p_np.png)
[ref](https://wkdtjsgur100.github.io/P-NP/)