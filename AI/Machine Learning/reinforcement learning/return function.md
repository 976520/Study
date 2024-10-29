## 대가 함수

1. 이해

시점 $t$에서 return은 episode의 모든 기간에 걸쳐 얻은 reward의 총합이다. $R_{t+1}=r$이 $t$에서 행동 $A_t$를 수행한 후 얻은 즉각적인 reword이라고 할 때, 다음으로 이어지는 reword은 $R_{t+2}, R_{t+3}, \cdots$이다. 이러한 reword들을 모두 더하면 시점 $t$에서의 return이 된다.

$$
G_t = R_{t+1} + R_{t+2} + R_{t+3} + \cdots = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}
$$

여기서 $\gamma$는 discount factor이다. 이 값은 0보다 크고 1보다 작으며, 현재 시점에서 미래 reword이 얼마나 가치 있는지 나타낸다. $\gamma=0$이면, 미래 reword를 고려하지 않는다는 의미이고, $\gamma=1$이면, return은 모든 미래의 reward를 그대로 모두 더한 값이 된다.

---
