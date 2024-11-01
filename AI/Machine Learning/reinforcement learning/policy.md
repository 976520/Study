## 정책

1. 이해

   Policy는 다음에 선택할 action을 결정하는 함수이다. 이는 결정적일 수도 있고, 확률적일 수도 있다는 특징이 있다. 확률적 policy는 주어진 state에서 agent가 선택할 수 있는 action에 대한 확률 분포를 가진다.

   $$
   \pi(a|s)=P[A_t=a|S_t=s]
   $$

2. optimal policy

   학습 중에 agent가 더 많은 경험을 얻으면 policy가 바뀔 수 있다. 만약 처음에 agent가 모든 action의 확률이 균등한 policy로 시작했다면, agent는 optimal policy에 가깝게 되도록 학습을 할 것이다. 이때 optimal policy는 가장 높은 return을 만드는 policy로, $\pi^*(a|s)$로 표현한다.

---
