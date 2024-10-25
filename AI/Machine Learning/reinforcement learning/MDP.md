# Markov Decision Process

> Markov decision process는 discrete time stochastic control process(이산 시간 확률 제어 과정)이다.

---

## Markov prosess

1. 이해

   > Markov prosess는 markov property를 가진 discrete time stochastic process(이산 시간 확률 과정)이다.

   Markov chain과 같은 의미이다.

   Markov prosess는 어떤 state가 일정한 간격으로 변화하고, 다음 state $S_{t+1}$가 현재 state $S_{t}$에만 의존하여 확률적으로 변화하는 것을 뜻한다. 즉, $S_{t+1}$에는 $S_{t}$만이 영향을 미칠 수 있으며, 그 이전 history는 영향을 미치지 않는다. 때문에 과거와 현재의 state를 모두 고려 했을 때 미래의 state가 나타날 확률과 현재의 state만 고려했을 때 미래의 state가 나타날 확률이 동일하다. 이를 수식으로 나타내면 다음과 같다.

   > $P(S_{t+1} | S_{t}) = P(S_{t+1} | S_{t}, ..., S_{t-1}, S_{t})$

   이러한 성질을 markov property라고 한다. **Markov property은 $S_{t}$가 $S_{t+1}$를 결정하는 데 필요한 모든 정보를 포함하고 있다는 것**을 의미한다. 따라서 과거의 상태는 현재의 상태를 통해 간접적으로만 영향을 미치게 된다.

   **Markov prosess는 시간 $t$에 따른 state $S_{t}$의 변화**를 나타내고, 이 상태의 변화를 transition(전이)이라고 한다. 이러한 변화를 확률로 표현하면 state transition probability(상태 전이 확률)이라고 한다.

   $t$에서의 상태를 $s$라고 하고, $t+1$에서의 상태를 $s'$라고 하면, $s$에서 $s'$로 이동할 확률 state transition probability $P_{ss'}$는 conditional probability(조건부 확률)를 이용해 다음과 같이 나타낼 수 있다.

   > $P_{ss'} = P(S_{t+1} = s' | S_{t} = s)$

   이에 대한 조건은 다음과 같다.

   1. 상태 $s$에서 상태 $s'$로 transition할 probability가 존재한다.

      > $P_{ss'}>0$

   2. 상태 $s$에서 가능한 모든 $s'$로의 transition probability의 합은 1이다.

      > $\sum_{s' \in S} P_{ss'} = 1$

      즉, 상태 $s$에서 반드시 어떤 상태 $s'$로 transition하게 된다.

2. State transition diagram

   State transition diagram은 모든 state와 state transition probability를 나타낸 directed graph이다.

   <img src="https://github.com/user-attachments/assets/64d2ec4f-2564-4191-b2fe-567a06bb4f98" width="500">

   위 transition diagram에서는 각 원이 state $s$를 나타내고, 화살표는 state transition을 의미하며, 화살표의 숫자로 state transition probability $P_{ss'}$를 나타낸다.

   `독서`에서 `웹 서핑`, `취침`으로 이동할 확률을 모두 더하면 1이 나온다. 이처럼 하나의 state에서 다른 state로 이동할 확률의 총합은 1인 것을 알 수 있다. 그리고 `취침`은 종료 state이기 때문에 다른 state로 이동할 확률은 0이다.

3. State transition probability matrix

   > State transition probability matrix는 모든 state의 전이 확률을 나타낸 행렬이다.

   State transition diagram를 행렬로 표현한 것이다. 각 행의 합이 1인 것을 확인할 수 있다.

   > $S_{t} =$ $\begin{bmatrix}
   > 0 & 0.1 & 0.1 & 0.8 & 0 \\ 
   > 0 & 0 & 0.3 & 0 & 0.7 \\
   > 0.1 & 0.2 & 0.2 & 0 & 0.5 \\
   > 0.6 & 0 & 0 & 0.4 & 0 \\
   > 0 & 0 & 0 & 0 & 1 \\
   > \end{bmatrix}$

   $S_t$가 `독서`, $S_{t+1}$이 `취침`일 때 $P_{ss'} = 0.7$이다. 즉, `취침` state의 결정에 있어 `독서`가 70%의 확률로 영향을 미치며, `웹 서핑`이 30%의 확률로 개입하는 것을 알 수 있다. 이처럼 $S_{t+1}$을 결정하는 데에 $S_{t}$가 높은 확률로 영향을 미칠 뿐, 다른 random variable(확률 변수)가 전혀 개입하지 않는 것은 아니다.

---

## Markov Reward Process

Markov process는 현재 state만이 다음 state를 결정하는 것이라면, Markov reward process는 현재 state와 다음 state의 보상을 고려하여 다음 state를 결정하는 것이다.
