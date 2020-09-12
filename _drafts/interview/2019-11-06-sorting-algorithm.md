---
layout: post
mathjax: true
title: Sorting algorithms
tags: [Basic concept, CS]
excerpt_separator: <!--more-->
---

알고있는 sort 알고리즘에 대해 말하고 설명해보라. time complexity는? merge sort에 대해서 설명해보라. time complexity는? O(n log n) 보다 빠른 정렬 알고리즘은 없는가? 가능하다면 어떻게 할 수 있는가.

<!--more-->

Sorting algorithm은 time complexity에 따라 크게 두 가지로 나누어진다.

- $O(n^2)$: Bubble sort, selection sort, insert sort
- $O(n \log{n})$: Merge sort, Heap sort, Quick sort

각 sorting algorithm 의 동작방식

- Bubble sort: 
	- 바로 옆에 있는 것 끼리 비교해나가면서 자리를 바꾼다
	- 한 번 쭉 도는데 복잡도 $n$, 그걸 $n$ 번 수행해야하기때문에 $n^2$
- Selection sort
	- 한번 쭉 훝은다음에 젤 작은거 찾아서 첫번째에 둠. 이걸 n개에 대해서 수행함.
	- 한번 훝은데 $n$ 이걸 $n$에 대해서 해야해서 $n^2$
	- 근데 사실 훝는데 정확히 $n$ 이라기 보다는 $n-k$ 라고 봐야하지만, 평균내면 $\frac{\sum k}{n}$ 은 어짜피 $n$에 비례함. 그래도 bubble sort 보다 좋긴 함
- Insert sorting
	- 앞에서부터 하나씩 골라서 적절한 위치에 끼워넣음

두번째 친구들

- Merge sort
	- Complexity: $O(n \log n)$ Devide를 반씩 나누어서 내려가기 때문에 depth 는 $\log{n}$, 각 level에서의 연산은, 이미 아래에서 한번 정렬되어 올라오기때문에 $n$ 번의 비교로 정렬 가능함 ([그림 출처](https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html))
	![complexity](https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort-concepts.png)
- Heap sort
	- 자료를 저장하는 구조인 heap 트리를 활용
		- heap tree 는 루트에 최대값 (또는 최소값)을 항상 유지하며 부모노드의 값이 자식보다 항상 크다(또는 작다)는 조건을 만족하는 자료 구조
	- 기본적으로 하고 싶은건 selection sort 같은 거야. 최대값을 훝어서 하나씩 채워넣을거야. 근데 최대값을 하나 찾아서 다음꺼 찾는 과정이 $\log n$ 의 복잡도를 가지고, 그걸 $n$ 개의 값에 대해서 정렬해야해서 $n\log{n}$이 나옴
- Quick sort
	
 



