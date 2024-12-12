## 가치 함수

1. return function

   1. 이해

      시점 $t$에서 return은 episode의 모든 기간에 걸쳐 얻은 reward의 총합이다. $R_{t+1}=r$이 $t$에서 action을 수행한 후 얻은 즉각적인 reword이라고 할 때, 다음으로 이어지는 reword은 $R_{t+2}, R_{t+3}, \cdots$이다. 이러한 reword들을 모두 더하면 시점 $t$에서의 return이 된다.

      $$
      G_t = R_{t+1} + R_{t+2} + R_{t+3} + \cdots = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}
      $$

      여기서 $\gamma$는 discount factor이다. 이 값은 0보다 크고 1보다 작으며, 현재 시점에서 미래 reword이 얼마나 가치 있는지 나타낸다. $\gamma=0$이면, 미래 reword를 고려하지 않는다는 의미이고, $\gamma=1$이면, return은 모든 미래의 reward를 그대로 모두 더한 값이 된다.

   2. return function의 재귀적 표현

      이 return function을 재귀적으로 표현하여 다음과 같이 쓸 수 있다.

      $$
      G_t = R_{t+1}+\gamma G_{t+1} = r + \gamma G_{t+1}
      $$

      이는 시점 t에서 return이 즉각적인 보상 $r$과 다음 시점 $t+1$에서 discount factor이 적용된 미래의 return을 더한 것이라는 의미이다.

2. policy function

   1. 이해

      Policy는 다음에 선택할 action을 결정하는 함수이다. 이는 결정적일 수도 있고, 확률적일 수도 있다는 특징이 있다. 확률적 policy는 주어진 state에서 agent가 선택할 수 있는 action에 대한 확률 분포를 가진다.

      $$
      \pi(a|s)=P[A_t=a|S_t=s]
      $$

   2. optimal policy

      학습 중에 agent가 더 많은 경험을 얻으면 policy가 바뀔 수 있다. 만약 처음에 agent가 모든 action의 확률이 균등한 policy로 시작했다면, agent는 optimal policy에 가깝게 되도록 학습을 할 것이다. 이때 optimal policy는 가장 높은 return을 만드는 policy로, $\pi^*(a|s)$로 표현한다.

3. state-value function

   강화학습에서 agent는 reword를 많이 받는 행동을 선택하도록 학습한다. 보상은 action을 수행한 후 다음 state에서 제공되므로, 이처럼 받지 않은 reword를 고려해야 한다.

   State value function은 특정 상태가 궁극적인 목표를 달성하는데 있어서 얼마나 좋은지 나쁜지를 측정하는 척도이다. 이는 return을 기준으로 한다.

   상태 $s$의 value function을 policy $\pi$를 따른 후 모든 episode에 걸친 평균 return $G_t$의 기댓값 $v_\pi(s)$는 다음과 같다.

   $$
   v_\pi(s) = E_\pi[G_t|S_t=s]=E_\pi[\displaystyle\sum_{k=0}\gamma^{k+1}R_{t+k+1}|S_t=s]
   $$

   현재 state에서 한 episode가 끝날 때까지 받은 reword의 합을 통해 현재 state의 value를 측정할 수 있다. 하지만 reword의 단순 합으로 value function을 작성하면 시간 개념을 적용할 수 없다는 단점이 있다. 따라서 discount factor $\gamma$를 곱해 미래의 reword를 discount하여 return을 구하는 것이다. Reword가 확률변수임에 따라 return도 확률변수이기 때문에 평균을 의미하는 기댓값을 취하여 value function을 유도하는 것이다.

4. bellman equation

   $v_\pi(s)$는 다음과 같이 재귀적으로 표현할 수 있으며,

   $$
   v_\pi(s) = E_\pi[R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}+\cdots|S_t=s] = E_\pi[R_{t+1}+\gamma v_{\pi}(S_{t+1})|S_t=s]
   $$

   $$
   v_\pi(s) = \sum_{a\in A}\pi(a|s)\sum_{s'\in S}p(s'|s,a)[R(s,a,s')+\gamma v_\pi(s')]
   $$

   이를 bellman equation이라고 한다. 이 방정식은 현재 상태의 가치를 immediate(즉각적) reward $R(s,a,s')$과 다음 상태의 discounted(할인된) value $\gamma v_\pi(s')$의 합으로 표현한다.

5. action-value function

   State-value function을 통해 다음 state들의 value를 판단할 수 있으며, agent는 이를 바탕으로 더 value가 높은 state로 가기 위한 action을 선택하여 state를 transition하게 된다.

   하지만 여기서 다음과 같은 문제가 발생한다.

   1. Agent가 다음에 도달할 수 있는 모든 state들의 정보를 미리 알고 있어야 한다.

   2. 특정 action을 선택하더라도 원하는 state로 항상 이동할 수 있다는 보장이 없다. 즉, state transition probability를 고려해야 한다.

   때문에 action에 대한 value function이 필요하다. Action-value function은 state-action pair에 대해 value를 정의한 것으로, 특정 state에서 취한 action이 얼마나 좋을 지 판단하는 것이다.

   상태 $s$에서 선택한 행동 $a$에 대한 return $G_t$의 기댓값 $q_\pi(s,a)$는 다음과 같다.

   $$
   q_\pi(s,a) = E_\pi[G_t|S_t=s,A_t=a] = E_\pi[\displaystyle\sum_{k=0}\gamma^{k+1}R_{t+k+1}|S_t=s,A_t=a]
   $$

---
