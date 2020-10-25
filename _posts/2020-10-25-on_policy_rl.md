---
layout: post
mathjax: true
title: What Matters in On-Policy RL
tags: [Reinforcement learning, Paper]
ref: 2020-10-25-on_policy_rl
lang: kr
excerpt_separator: <!--more-->
---
[Paper review] On-policy 강화학습을 하는데 중요한 것은? 

<!--more-->

{% include aligner.html images="review/on_policy_rl/title.png" column=1 %}



Google Brain 팀에서 ["What Matters In On-Policy Reinforcement Learning? A Large-Scale Empirical Study."](https://arxiv.org/pdf/2006.05990.pdf) 이라는 논문을 썼는데요, 강화학습, 특히 여기서는 on-policy 방식의 학습을 진행할 때, 성능에 영향을 미치는 요소들에 대해서 정리해주는 재미있는 논문입니다. 강화학습을 할 때 꼭 확인해야할 체크리스트를 제공해주는 느낌도 있어서 여기서 이야기 하고 있는 것들을 한번 정리해보려고 합니다.


-----------------------------

## Motivation


최근까지도 정말 다양한 강화학습 관련 연구들이 진행되고 있습니다. 논문의 저자들은 주어진 환경에서 학습의 성능을 개선하기 위한 다양한 아이디어들을 제시하고 실제로 실험으로 제시한 알고리즘을 검증합니다. 하지만 독자 입장에서 논문의 아이디어를 재구현해서 실험해보면 논문에서 제시하고 있는 성능을 비슷하게 달성하는 것이 어려운 경우가 종종있습니다. 논문쓸 때, 기존연구와 비교를 하고싶은데 논문에서는 잘 된다고 하는데 내가 구현하면 잘 안되서 비교하기가 힘든 경우가 종종 있죠. 


일반적으로 재검증이 힘든 이유는 논문에서 제시한 아이디어가 개념적으로는 매우 간단하더라도, 이것을 잘 동작하도록 하는 구현에는 다양한 디자인 결정들이 있어야 하기 때문입니다. 예를 들어 뉴럴 네트워크의 구조, learning rate 등 기본적인것 부터 시작해서 mini-batch size, 뉴럴 네트워크의 초기값 등 매우 사소한 것들까지 다양한 요소들을 잘 결정해주어야 원하는 성능을 달성할 수 있습니다. 물론 친절한 저자들은 코드와 모든 세팅을 공유해주기도 합니다. 하지만 우리가 테스트하고자 하는 환경이 조금 달라진다면? 결국 이런 요소들을 다시 결정해주어야 하고 이 때 잘 결정하는 것이 성능에 큰 영향을 미치게 됩니다.


물론 머신러닝 모델 학습은 다 노가다라고는 하지만, 노가다를 어떻게 하면 효율적으로 할 수 있을지에 대해서는 항상 많은 고민이 있습니다. 이 논문은 이런 고민에 대한 정답까지는 아니더라도 어디서 어떻게 시작하면 좋을지 가이드라인을 제시해주고 있습니다. 고맙게도 다양한 요소들을 바꾸어가면서 실험을 한 결과를 정리해서 대충 어떤 세팅부터 시작해보면 좋을지 정리해서 너무나 친절하게 알려주고 있습니다.

다시 정리해보면, 이 논문에서는 5개의 기본적인 환경(그러나 서로 다른 복잡도를 가지고 있는)에서 50개가 넘는 크고 작은 디자인 결정들이 강화학습(특히 on-policy RL in continuous control tasks)의 최종 성능에 어떤 영향을 미치는지 실험을 통해 보여주고, 학습 진행에 대한 직관과 가이드라인을 주고 있습니다.

<!-- 논문들에서 중요한 결정들(뉴럴 네트워크 구조 또는 learning rate 등)을 공유해주기도 하지만 사실 그보다 훨씬 마이너한 요소들(그렇지만 성능에는 영향을 미칠 수도 있는) 모두 공유해주지는 못하는 경우도 있고, environment에 따라 최적의 디자인 결정들이 달라질 수 있기때문에 사용하고자 하는 알고리즘에 잘 맞는 디자인 결정들을 잘 찾아야 좋은 결과를 얻을 수 있습니다.  이 논문에서는 강화학습 (특히 on-policy RL in continuous control tasks)에서 어떤 요소들이 성능에 어떤 영향을 미치는지 다양한 실험을 통해서 보여주고 있습니다. 물론 5개의 간단한 환경에서 실험을 한 결과를 보여주고 있기때문에 모든 상황으로 일반화 할 수 있는 결과는 아니지만 알고리즘의 핵심 컨셉 이외에도 이 논문에서 실험하고 있는 다양한 요소들이 성능에 큰 영향을 미친다는 것을 확인하고, 좋은 결정을 하기위한 약간의 가이드라인을 제시해주고 있습니다. 그리고 한가지 발견은 초기값 세팅이 성능에 매우 중요한 영향을 미친다는 것 입니다.      여기서 타겟으로 하고있는것은 on-policy RL in continuous control tasks.
 **Contribution of this paper**
 이 논문의 목표는 크고 작은 디자인 결정들이 최종 성능에 어떤 영향을 미치는지 실험을 통해 보여주는 것입니다. 
50개가 넘는 디자인 결정들을 설정하고 이를 바꾸어가면서 매우 많은 실험을 진행하였고 이 실험결과에 대한 분석과 학습 진행에 대한 직관을 제공합니다.-->
 
## Study Design

**Tested environment.** 이 논문에서는 OpenAI Gym에서 제공하는 대표적인 continuous control 작업인 다음의 5개의 환경에서 테스트를 진행했습니다. 
Hopper-v1, Walker2d-v1, HalfCheetah-v1, Ant-v1, Humanoid-v1
 
![Ant](https://github.com/aipasta/aipasta.github.io/blob/master/assets/img/review/on_policy_rl/ant.gif?raw=true){: width="50%" height="50%"}![Humanoid](https://github.com/aipasta/aipasta.github.io/blob/master/assets/img/review/on_policy_rl/humanoid.gif?raw=true){: width="50%" height="50%"}

**Unified on-policy learing algorithm.** 다양한 알고리즘들을 공정하게 비교하기 위해서는 동일한 환경에서 학습되고 그 결과를 비교할 수 있어야 한다. 이를 위해서 저자들은 configuration 설정에 따라 다양한 방식으로 동작할 수 있는 통합된 학습 알고리즘을 먼저 구현했습니다. PPO 논문에 나온 실험결과와의 비교를 통해 이 알고리즘이 잘 동작하는지 검증한 뒤 실험을 진행하였습니다. 이렇게 통합된 알고리즘을 구현하면서 생겼던 디자인 결정들을 모두 테스트 해야할 parameter로 정의해서 50개가 넘는 요소들을 정의하고 이들에 대한 모든 실험을 진행하였다고 하네요.

## Experiments

앞서 이야기 했듯이, 이 논문에서는 50개가 넘는 디자인 결정들에 대해 매우 많은 실험을 진행하였는데 크게 8개의 카테고리로 나누어 볼 수 있습니다. 각각에 대해 결과를 이야기 해보겠습니다. 
> 참고로 제 의견은 이 폰트로 표시해두었습니다. 사실이 아닐 수 있습니다.

### 1. Policy losses

**Design Decisions.**
우선 첫번째로 어떤 loss로 모델을 학습할지 입니다. 모델을 학습할 때 어떤 loss function을 이용하여 학습할 것인지는 논문들이 제안하는 알고리즘들의 핵심 아이디어라고 할 수 있는데, 여기서는 크게 6개의 연구에서 제안했던 loss를 비교하고 있습니다. (Vanilla policy gradient, V-trace, PPO, AWR, V-MPO, RPA.)

<!--![Image of a glass on a book]({{ site.baseurl }}/assets/img/review/on_policy_rl/r1.png)-->

{% include aligner.html images="review/on_policy_rl/r1.png" column=1 %}

**Interpretation & Recommendation.** 위의 그림에서 볼 수 있듯이 PPO가 모든경우에 잘 동작하고 있다는 것을 확인할 수 있습니다.

1. On-policy 강화학습에서는 PPO policy loss 가 대부분의 환경에서 추천할만하다.
2. 이 때, PPO clipping threshold 값은 0.25에서 시작해서 튜닝해나가는 것이 좋다.

> 이 논문의 단점은 왜 그런것인지 알려주지 않는다는 것인데, 이건 아마 자기들도 몰라서 그런 듯... 지금 테스트하고 있는 환경의 특성때문에 특정 알고리즘이 더 잘 동작할 수도 있을텐데 정확히는 잘 모르겠네요. 저자들도 PPO가 항상 좋다는게 아니라 알고리즘에따라 이런 차이가 날 수 있다라는 이야기를 하고 있는 것이라고 하네요.



### 2. Networks Architecute

**Design decisions.** 
다음으로 결정해야하는 것은 뉴럴 네트워크의 구조입니다. 여기서 한 가지 확인하고 갈 것은 고려하고 있는 알고리즘들이 actor-critic 방식으로 학습이 되기때문에 policy(actor)와 value(critic) 이렇게 두 가지 값을 학습해야 합니다.
뉴럴 네트워크 구조 관련해서 결정해야할 것들은 다음과 같습니다.

- Shared structure: value와 policy 뉴럴 네트워크를 공유할 것인지 결정해야합니다. 기본적으로 value와 policy의 input은 같고 결과값 또한 서로 밀접한 관련을 가지고 있기때문에 만연 연구들에서 이 네트워크의 일부를 공유하는 방법을 많이 사용했습니다. (당연히 장단점이 있는데.. 나중에 ...)
- Neural network size: value/policy 각각의 neural network의 크기 (depth, width)를 결정해주어야 합니다.
- Activation: Activation함수는 어떤것으로 정해줄 것인가도 결정해야할 중요한 요소입니다. (e.g., ELU, Leaky ReLU, ReLU, Sigmoid, Swish, Tanh)
- Initialization of network weight: 뉴럴 네트워크의 초기값을 얼마로 결정할 것인가 결정해야합니다.

**Interpretation & Recommendation.**

- Shared structure: Separate, 공유하지 않고 서로 독립적인 뉴럴 네트워크를 가지고 있는 것이 더 좋은 성능을 얻었다고 합니다. <!--하는 것이 좋음. 당연히 장단점이 있을 것이라고 생각 (Prior to reading this study, I had the impression that sharing some layers between actor and critic is beneficial for the agent. I reasoned that parameter sharing could accelerate training (gradient flowing from both the actor and the critic). However, I have learned that the norm of gradients flowing back from the actor and the critic could be at completely different scale. As a result, actor’s gradients may destabilise critic’s parameters and vice-versa. This is probably the reason for keeping policy and value network separate.)-->
- Neural network width: (너무 당연하게도) 환경의 복잡도에 따라 달라지며 너무 작거나 너무 크면 성능저하가 생길 수 있습니다. 한 가지 재미있는 결과는 policy보다는 value를 더 넓게 하는게 더 좋은 성능을 준다고 합니다. 
> 이건 한번 이해를 해보자면, 아마도 value는 policy가 어떻게 행동할지를 고려해서 미래의 가치까지 예측해야하니깐 더 복잡한 모델이 필요할 수 있을 것 같습니다.
- Neural network depth: hidden layer가 두 개인 경우 대부분 좋은 성능을 얻었다고 합니다.
- Activation: 네트워크의 깊이가 그렇게 크지 않을 경우에 tanh 함수가 좋다고 합니다. *(왜 그런지는 잘 모르겠네요.)* <!--(relu 안좋음) 왜? if the network is not too deep. (Surprisingly, it is better to use tanh activations rather than ReLU between actor’s/critic’s MLP layers. But only networks with limited capacity shall benefit from it. Anecdotically, tanh activation tends to be more reliable when you have smaller networks. It learns faster and is less sensitive to big differences in input features than ReLU. 이건 몰랏던 사실인데) -->
- Initialization of network weight: 이것도 재미있는 결과인 것 같습니다. 처음 action의 확률분포가 평균 0 그리고 작은 표준편차(0.5 정도)를 갖도록 하면 좋다. (normalized action on [-1,1] 을 기준으로). 그리고 이걸 하는 방법은 뉴럴 네트워크의 마지막 레이어의 웨이트 값을 조절해주면 됩니다. 

<!--**Recommendation**
- Policy 뉴럴 네트워크의 마지막 레이어 weight를 작은값으로 초기화 할 것.
- Value와 Policy
- Use softplus for transformation from policy output to action standard deviation-->

### 3. Normalization and Clipping

**Design decisions.** 다음으로 결정할 것은 normalization 입니다. 실제로 뉴럴 네트워크를 학습할 때 normalization은 항상 중요한데, 강화학습에서도 아마도 중요할 것 같습니다. 여기서는 다음의 것들을 실험하고 있네요.

- Observation normalization: obs를 평균($o_{\mu}$)을 빼고 표준편차($o_{\rho}$)로 나누어줍니다. 이렇게 해주면 obs는 평균 0, 표준편차 1인 분포와 비슷하게 만들어집니다.
- Value function normalization: 위와 비슷하게 value network를 학습할 때 target value ($\hat{V}$)를 평균($v_{\mu}$)을 빼고 표준편차($v_{\rho}$)로 나눈 normalized target value 를 이용해서 학습합니다. 
- 이 외에도 Per minibatch advantage normalization, Gradient clipping and observation  기법들을 테스트 해봅니다.

**Interpretation & Recommendation.** 간단하게 다음과 같이 정리할 수 있을것 같네요.
- Input normalization: 꼭 하세요
- Value function normalization: 가능하면 하세요.
- Gradient clipping: 하면 성능은 개선될텐데 그렇게 중요하지는 않음.
- per-minibatch advantage normalization, observations clipping: 큰 차이 없음.




### 4. Advantage Estimation

**Design decisions.**  Advantage estimators(e.g. GAE, N-step)의 결정과 각각에 대한  hyperparameters의 선정이 성능에 어떤 영향을 미치는지 실험했습니다.

**Recommendation.**
On-policy 환경에서는, GAE 가 좋은 성능을 내고 $\lambda=0.9$ 값을 초기값으로 해서 시도해보면 좋을 것 같습니다.


### 5. Training Setup

**Design decisions.** 학습을 잘 하기위해서는 학습 하는 방법에 대한 세팅도 당연히 중요하겠습니다. 여기서는 크게 다음의 5가지를 바꾸어가면서 실험 한 결과를 보여주고 있는데 한가지 흥미로운 결과를 보여주고 있습니다.
- Number of parallel environments: 한번에 병렬로 실행하는 환경의 개수. A3C 같은 알고리즘에서는 현재의 policy를 여러 개의 환경에서 한꺼번에 실행하고, 거기서 얻은 샘플들을 이용해서 policy를 업데이트 하게되는데, 이 때 한번에 몇개의 환경을 병렬적으로 동시에 돌릴 것인지 결정해야 합니다.
- Number of transitions gathered in each iteration: 현재 policy를 이용하여 반복적으로 action을 취해보고 (one-iteration) 샘플들을 모으게 되는데 그 다음 policy 업데이트 하기전까지 반복하는 회수(즉, 모으는 샘플의 개수)를 의미합니다.
- Number of passes over the data: 한번 수집한 데이터를 몇번 반복하여 학습에 사용할 것인지 결정해야 합니다.
- Mini batch size: batch로 묶어서 보통 연산을 하는데, 이때 적절한 사이즈는 어떻게 되는지. 

<!--![Analysis of choice num_envs]({{ site.baseurl }}/assets/img/review/on_policy_rl/num_env.png)-->

{% include aligner.html images="review/on_policy_rl/num_env.png" column=1 %}

**Interpretation & Recommendation.** 먼저 가장 흥미로운 결과부터 이야기를 해보면 number of parallel environments에 대한 것입니다. 위의 그래프가 이 결과를 보여주고 있는데, 환경의 개수가 너무 커지면 오히려 성능이 저하되는 경우가 있는 것을 볼 수 있습니다. 또한 number of iteration 결과도 비슷한 양상을 보여주는데, 어느정도(1024~2048 iteration)까지는 성능이 좋아지지만 이것보다 커지면 오히려 나빠지는 것을 확인했습니다.

> 당연하게도 이 값은 크면 클수록 더 빨리 좋은 성능을 달성할 것으로 생각했는데, 결과는 예상과는 다르게 나왔네요. 물론 너무 큰 값에서는 잘 동작하지 않겠지만, 제가 예상했던 것 값보다는 상대적으로 작은 값부터 성능이 나빠지기 시작했습니다. 저는 off-policy기준으로 생각했을 때, 독립적인 환경에서 온 많은 샘플들이 도움이 많이 되었기 때문에 여기서도 마찬가지라고 생각했습니다. 하지만 PPO와 같은 알고리즘에서는 많은 샘플이 오히려 최적화과정을 어렵게 만들어서 성능이 오히려 나빠지게 된다고 합니다.

그 외에는 당연한 결과들을 얻었는데, 한번의 경험을 여러번 사용하는것은 성능향상에 도움이 됩니다. 그리고 batch size는 이 논문에서는 실험해본 256까지는 성능 저하가 전혀 없어서 저자는 컴퓨터의 성능이 허락한다면 이정도까지 늘려서 성능저하없이 속도를 빠르게 하는 것을 추천합니다.

### 6. Timesteps Handling

**Design decisions** 다음은 시간과 관련된 결정들입니다. 강화학습에서 빼놓을 수 없는 discount factor $\gamma$를 결정해야 합니다. 그리고 frame skip, 즉 매 프레임마다 학습을 할 것인지 아니면 어느정도 간격을 두고 할 것인지 또한 결정해야할 요소 입니다.
> Discount factor는 문제에서 주어지는 경우도 있지만 이 [논문](https://arxiv.org/pdf/2007.02040.pdf)[^1]에서 처럼 학습 성능 개선을 위한 방법으로도 쓰이기도 합니다. 따라서 후자의 경우를 생각해보면 이것도 성능의 영향을 미치는 결정해야한 요소라고 할 수 있습니다. 

**Interpretation & Recommendation.**

- Discount factor  $\gamma$: 성능에 매우 큰 영향을 미치며 실험한 환경에서는 0.99를 시작으로 튜닝해 가는 것이 좋을 것 같다는 결과를 얻었습니다.
- Frame skipping 은 상황에 따라 도움이 되는 경우도 있고 아닌 경우도 있습니다.


### 7. Optimizers

**Design decisions.** Adam, RMSprop와 같은 다양한 gradient-based optimizers들을 사용할 수 있습니다. 어떤 optimizer를 사용할지 또한 각각에 대해 hyperparameters를 어떻게 설정할지를 결정해야 합니다.

**Interpretation & Recommendation.**
Adam optimizer (momentum $\beta_1=0.9$, learning rate $0.0003$)로 설정하여 시작하는 것을 추천합니다. 또한 시간이 갈수록 linear하게 learning rate 를 낮추어 가는것이 성능향상에 조금 도움이 된다는 결과를 얻었습니다.

### 8. Regularization

**Design decisions.** 마지막으로 regularizers입니다. 일반적으로 policy gradient기반의 방식에서는 regularization이 성능에 agent가 exploration을 잘 할수 있도록 하여 성능에 큰 도움이 되는 것으로 알려져 있습니다. 

**Interpretation & Recommendation.**
Entropy, KL divergence between action distribution, unit Gaussian 등의 방법을 실험해 보았지만 큰 도움이 되지 않았습니다. 논문에서는 그 이유로 두가지를 들고 있습니다.
1. PPO의 policy loss가 이미 regularization 비슷한 역할을 수행하고 있다는 점.  
2. 앞서 이야기했던 뉴럴네트워크의 초기값 설정이 이미 효율적인 exploration을 보장하는 점.
따라서 on-policy 기반의 강화학습을 사용할때는 regularization에는 크게 신경쓰지 않고 학습을 진행해도 될 것 같습니다.


## 정리 및 결론

이 논문은 강화학습에 어떤 요소가 영햐을 미치는 지를 방대한 실험으로 보여주고 이에 대한 해석 및 학습 가이드라인을 제시하고 있습니다. 논문의 supplementary 에서는 무려 40페이지가 넘는 양의 실험 결과를 보여주고 있습니다. 자세한 결과는 논문을 확인하면 잘 설명되어 있습니다.

이 논문은 실제로 강화학습을 이용해 학습을 하는 사람들에게 큰 도움이 될 것 같습니다. 당연하게도 논문에서 얻은 결과는 사실 새로운 환경이나 알고리즘에 바로 적용하기는 힘들 수 있습니다. 하지만 적어도 성능을 최적화하기 위해서 우리가 어떤 요소들을 고려해야하는지에 대한 체크리스트를 제공해주고 있습니다. 또한 각각의 hyperparameter를 어떤 값부터 시작해야할지 막막한 경우가 많은데 어떻게 search해 가야하는지 시작점을 정하는데에도 큰 도움이 될 것 같습니다.

끝

---------------
[^1]: Amit, Ron, Ron Meir, and Kamil Ciosek. "Discount Factor as a Regularizer in Reinforcement Learning." arXiv preprint arXiv:2007.02040 (2020).