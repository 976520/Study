# Markov Decision Process

> Markov decision process는 discrete time stochastic control process(이산 시간 확률 제어 과정)이다.

---

## Markov prosess

1. 이해

   > Markov prosess는 markov property를 가진 discrete time stochastic process(이산 시간 확률 과정)이다.

   Markov chain과 같은 의미이다.

   Markov prosess는 어떤 state가 일정한 간격으로 변화하고, 다음 state $S_{t+1}$가 현재 state $S_{t}$에만 의존하여 확률적으로 변화하는 것을 뜻한다. 즉, $S_{t+1}$에는 $S_{t}$만이 영향을 미칠 수 있으며, 그 이전의 history는 영향을 미치지 않는다. 때문에 과거와 현재의 state를 모두 고려 했을 때 미래의 state가 나타날 확률과 현재의 state만 고려했을 때 미래의 state가 나타날 확률이 동일하다. 이를 수식으로 나타내면 다음과 같다.

   > $P(S_{t+1} | S_{t}) = P(S_{t+1} | S_{t}, ..., S_{t-1}, S_{t})$

   이러한 성질을 markov property라고 한다. Markov property은 $S_{t}$가 $S_{t+1}$를 결정하는 데 필요한 모든 정보를 포함하고 있다는 것을 의미한다. 따라서 과거의 상태는 현재의 상태를 통해 간접적으로만 영향을 미치게 된다.

   Markov prosess는 시간 $t$에 따른 state $S_{t}$의 변화를 나타내고, 이 상태의 변화를 transition(전이)이라고 한다. 이러한 변화를 확률로 표현하면 state transition probability(상태 전이 확률)이라고 한다.

   $t$에서의 상태를 $s$라고 하고, $t+1$에서의 상태를 $s'$라고 하면, $s$에서 $s'$로 이동할 확률 state transition probability $P_{ss'}$는 조건부 확률을 이용해 다음과 같이 나타낼 수 있다.

   > $P_{ss'} = P(S_{t+1} = s' | S_{t} = s)$

   이에 대한 조건은 다음과 같다.

   > $P_{ss'}>0$

   > $\sum_{s' \in S} P_{ss'} = 1$

2. State transition probability matrix

   State transition diagram은 모든 state와 state transition probability를 나타낸 directed graph이다.

   <img src="https://github.com/user-attachments/assets/64d2ec4f-2564-4191-b2fe-567a06bb4f98" width="500">

   위 transition diagram에서는 각 원이 state를 나타내고, 화살표는 state transition을 의미하고, 화살표의 숫자로 state transition probability를 나타낸다.

   State transition probability matrix는 모든 state의 전이 확률을 나타낸 행렬이다. 이를 통해 $S_{t}$에서 $S_{t+1}$로 transition 할 확률을 쉽게 계산할 수 있다.

---

## Markov Reward Process
