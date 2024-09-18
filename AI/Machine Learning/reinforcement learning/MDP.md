# Markov Decision Process

> Markov decision process는 discrete time stochastic control process(이산 시간 확률 제어 과정)이다.

---

## Markov prosess

1. 이해

   > Markov prosess는 discrete time stochastic process(이산 시간 확률 과정)이다.

   Markov chain과 같은 의미이다.

   Markov prosess는 어떤 state가 일정한 간격으로 변화하고, 다음 state $S_{t+1}$가 현재 state $S_{t}$에만 의존하여 확률적으로 변화하는 것을 뜻한다. 즉, $S_{t+1}$에는 $S_{t}$만이 영향을 미칠 수 있으며, 그 이전의 history는 영향을 미치지 않는다. 때문에 과거와 현재의 state를 모두 고려 했을 때 미래의 state가 나타날 확률과 현재의 state만 고려했을 때 미래의 state가 나타날 확률이 동일하다. 이를 수식으로 나타내면 다음과 같다.

   > $P(S_{t+1} | S_{t}) = P(S_{t+1} | S_{t}, ..., S_{t-1}, S_{t})$

   이러한 성질을 markov property라고 한다. Markov property은 현재의 상태가 미래의 상태를 결정하는 데 필요한 모든 정보를 포함하고 있다는 것을 의미한다. 따라서 과거의 상태는 현재의 상태를 통해 간접적으로만 영향을 미치게 된다.

   Markov prosess는 시간 $t$에 따른 state $S_{t}$의 변화를 나타내고, 이 상태의 변화를 transition(전이)이라고 한다. 이러한 변화를 확률로 표현하게 되는데, 이를 state transition probability(상태 전이 확률)이라고 한다.

   $t$에서의 상태를 $s$라고 하고, $t+1$에서의 상태를 $s'$라고 하면, state transition probability $P_{ss'}$는 조건부 확률을 이용해 다음과 같이 나타낼 수 있다.

   > $P_{ss'} = P(S_{t+1} = s' | S_{t} = s)$

---

## Markov Reward Process
