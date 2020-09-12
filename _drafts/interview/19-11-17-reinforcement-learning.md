---
layout: post
mathjax: true
title: Reinforcement Learning
tags: [Basic concept, statistics]
excerpt_separator: <!--more-->
---

<!--more-->

- What is dynamic programming?
	- Dynamic sequential or temporal component to the problem 
	- Programming optimising a “program”, i.e. a policy
	- A method for solving complex problems by breaking them down into subproblems
		- Solve the subproblems
		- Combine solutions to subproblems
	- DP is general solution method the problem with following properties:
		- Optimal substructure: Principle of optimality applies (Optimal solution can be decomposed into subproblems)
		- Overlapping subproblems: Subproblems recur many times and solutions can be cached and reused
	- 그럼 DP 로 풀면 되는거 아님?
		- DP assumes full knowledge of the MDP (e.g., state transistion probability, reward)
	- Policy iteration and value iteration
		- Policy iteration: policy evaluation and policy improvement

Model free prediction

- MC vs TD
	- Bias/variance trade-off
	- Bootstrapping and Sampling
		- Bootstrapping: update involves an estimate (DP, TD)
		- Sampling: update samples an expectation (MC, TD)