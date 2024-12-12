## 가치 함수

1. state-value function

   강화학습에서 agent는 reword를 많이 받는 행동을 선택하도록 학습한다. 보상은 action을 수행한 후 다음 state에서 제공되므로, 이처럼 받지 않은 reword를 고려해야 한다.

   State value function은 특정 상태가 궁극적인 목표를 달성하는데 있어서 얼마나 좋은지 나쁜지를 측정하는 척도이다. 이는 return을 기준으로 한다.

   상태 $s$의 value function을 policy $\pi$를 따른 후 모든 episode에 걸친 평균 return $G_t$의 기댓값 $v_\pi(s)$는 다음과 같다.

   $$
   v_\pi(s) = E_\pi[G_t|S_t=s]=E_\pi[\displaystyle\sum_{k=0}\gamma^{k+1}R_{t+k+1}|S_t=s]
   $$

   현재 state에서 한 episode가 끝날 때까지 받은 reword의 합을 통해 현재 state의 value를 측정할 수 있다. 하지만 reword의 단순 합으로 value function을 작성하면 시간 개념을 적용할 수 없다는 단점이 있다. 따라서 discount factor $\gamma$를 곱해 미래의 reword를 discount하여 return을 구하는 것이다. Reword가 확률변수임에 따라 return도 확률변수이기 때문에 평균을 의미하는 기댓값을 취하여 value function을 유도하는 것이다.

2. bellman equation

   $v_\pi(s)$는 다음과 같이 재귀적으로 표현할 수 있으며,

   $$
   v_\pi(s) = E_\pi[R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}+\cdots|S_t=s] = E_\pi[R_{t+1}+\gamma v_{\pi}(S_{t+1})|S_t=s]
   $$

   $$
   v_\pi(s) = \sum_{a\in A}\pi(a|s)\sum_{s'\in S}p(s'|s,a)[R(s,a,s')+\gamma v_\pi(s')]
   $$

   이를 bellman equation이라고 한다. 이 방정식은 현재 상태의 가치를 immediate(즉각적) reward $R(s,a,s')$과 다음 상태의 discounted(할인된) value $\gamma v_\pi(s')$의 합으로 표현한다.

3. action-value funtion

   Action-value function은 state-action pair에 대해 value를 정의한 것으로, q function이라고 하기도 한다.

   상태 $s$에서 선택한 행동 $a$에 대한 return $G_t$의 기댓값

---
