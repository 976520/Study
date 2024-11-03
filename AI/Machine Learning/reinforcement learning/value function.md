## 가치 함수

1. state-value function

   state value function은 특정 상태가 얼마나 좋은지 나쁜지를 측정하는 척도이다. 이는 return을 기준으로 한다.

   상태 $s$의 value function을 policy $\pi$를 따른 후 모든 episode에 걸친 평균 return $G_t$의 기댓값으로 정의하면 다음과 같다.

   $$
   v_\pi(s) = E_\pi[G_t|S_t=s]=E_\pi[\displaystyle\sum_{k=0}\gamma^{k+1}R_{t+k+1}|S_t=s]
   $$

2. action-value funtion

---
