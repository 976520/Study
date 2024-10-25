# Markov Decision Process

> Markov decision process는 discrete time stochastic control process(이산 시간 확률 제어 과정)이다.

---

## Markov process

1. 이해

   > Markov process는 markov property를 가진 discrete time stochastic process(이산 시간 확률 과정)이다.

   정의된 확률 분포를 따라 state 사이를 이동하는 과정이다. 또한 markov chain과 같은 의미이다.

2. Markov property

   Markov process는 어떤 state가 일정한 간격으로 변화하고, 다음 state $S_{t+1}$가 현재 state $S_{t}$에만 의존하여 확률적으로 변화하는 것을 뜻한다. 즉, $S_{t+1}$에는 $S_{t}$만이 영향을 미칠 수 있으며, 그 이전 history는 영향을 미치지 않는다. 때문에 과거와 현재의 state를 모두 고려 했을 때 미래의 state가 나타날 확률과 현재의 state만 고려했을 때 미래의 state가 나타날 확률이 동일하다. 이를 수식으로 나타내면 다음과 같다.

   > $P(S_{t+1} | S_{t}) = P(S_{t+1} | S_{t}, ..., S_{t-1}, S_{t})$

   이러한 성질을 markov property라고 한다. **Markov property은 $S_{t}$가 $S_{t+1}$를 결정하는 데 필요한 모든 정보를 포함하고 있다는 것**을 의미한다. 따라서 과거의 상태는 현재의 상태를 통해 간접적으로만 영향을 미치게 된다.

3. State transition probability

   **Markov process는 시간 $t$에 따른 state $S_{t}$의 변화**를 나타내고, 이 상태의 변화를 transition(전이)이라고 한다. 이러한 변화를 확률로 표현하면 state transition probability(상태 전이 확률)이라고 한다.

   $t$에서의 상태를 $i$라고 하고, $t+1$에서의 상태를 $j$라고 하면, $i$에서 $j$로 이동할 확률 state transition probability $P_{ij}$는 conditional probability(조건부 확률)를 이용해 다음과 같이 나타낼 수 있다.

   > $P_{ij} = P(S_{t+1} = j | S_{t} = i)$

   이에 대한 조건은 다음과 같다.

   1. 상태 $i$에서 상태 $j$로 transition할 probability가 존재한다.

      > $P_{ij}>0$

   2. 상태 $i$에서 가능한 모든 $j$로의 transition probability의 합은 1이다.

      > $\sum_{j \in S} P_{ij} = 1$

      즉, 상태 $i$에서 반드시 어떤 상태 $j$로 transition하게 된다.

4. State transition diagram

   State transition diagram은 모든 state와 state transition probability를 나타낸 directed graph이다.

   <img src="https://github.com/user-attachments/assets/64d2ec4f-2564-4191-b2fe-567a06bb4f98" width="500">

   위 transition diagram에서는 각 원이 state $s$를 나타내고, 화살표는 state transition을 의미하며, 화살표의 숫자로 state transition probability $P_{ss'}$를 나타낸다.

   `독서`에서 `웹 서핑`, `취침`으로 이동할 확률을 모두 더하면 1이 나온다. 이처럼 하나의 state에서 다른 state로 이동할 확률의 총합은 1인 것을 알 수 있다. 그리고 `취침`은 종료 state이기 때문에 다른 state로 이동할 확률은 0이다.

5. State transition probability matrix

   > State transition probability matrix는 모든 state의 전이 확률을 나타낸 행렬이다.

   State transition probability matrix는 전체 markov process의 변화 추이를 나타낸다.

   State transition diagram를 행렬로 표현한 것이다. 모든 element가 0 이상 1 이하의 값을 가지며 각 row의 합이 1인 것(row stochastic)을 확인할 수 있다. 위의 예시 transition diagram에 대한 state transition probability matrix는 다음과 같다.

   > $Q =$ $\begin{bmatrix} 0 & 0.1 & 0.1 & 0.8 & 0 \\ 0 & 0 & 0.3 & 0 & 0.7 \\ 0.1 & 0.2 & 0.2 & 0 & 0.5 \\ 0.6 & 0 & 0 & 0.4 & 0 \\ 0 & 0 & 0 & 0 & 1 \\ \end{bmatrix}$

   $S_t$가 `독서`, $S_{t+1}$이 `취침`일 때 $P_{ij} = 0.7$이다. 즉, `취침` state의 결정에 있어 `독서`가 70%의 확률로 영향을 미치며, `웹 서핑`이 30%의 확률로 개입하는 것을 알 수 있다.

   이처럼 $S_{t+1}$을 결정하는 데에 $S_{t}$가 높은 확률로 영향을 미칠 뿐, 다른 random variable(확률 변수)가 전혀 개입하지 않는 것은 아니다. 이를 코드로 보면 다음과 같다.

   ```python
   import numpy as np

   Q = np.array([
       [0, 0.1, 0.1, 0.8, 0],
       [0, 0, 0.3, 0, 0.7],
       [0.1, 0.2, 0.2, 0, 0.5],
       [0.6, 0, 0, 0.4, 0],
       [0, 0, 0, 0, 1]
   ])

   # 현재 상태가 '독서' (index 1)일 때, 다음 상태가 '취침' (index 4)일 확률
   print(f"P(S_t+1 = '취침' | S_t = '독서') = {Q[1, 4]}") # 출력: 0.7

   # 현재 상태가 '독서' (index 1)일 때, 다음 상태가 '웹 서핑' (index 2)일 확률
   print(f"P(S_t+1 = '웹 서핑' | S_t = '독서') = {Q[1, 2]}") # 출력: 0.3
   ```

   또한 state transition probability matrix와 현재 state를 알고 있다면 전체 markov process의 state를 구할 수 있다. 현재 시점 $t$에 대한 state $S_t$가 $(1\times M)$ 행렬인 분포 $\vec{v}$를 따를 때,

   > $P(S_{t+1} = j) = \displaystyle\sum_{i \in S} P(S_{t+1} = j | S_t = i)P(S_t = i)$

   이는 내적을 이용하여 다음과 같이 나타낼 수 있다.

   > $\displaystyle\sum_{i \in S} v_{i} \times q_{ij}$ = $\vec{v}Q$

   이때 $v_i$는 $(1\times M)$ 행렬이고, $q_{ij}$는 $(M\times M)$ 정방행렬이다. 따라서 $t+1$ 시점의 transition probability matrix는 $(1\times M)$의 $\vec{v}Q$가 된다.

   $t+2$ 시점의 경우에는 다음과 같은데,

   > $P(S_{t+2} = k|S_{t} = i) = \displaystyle\sum_{j \in S} P(S_{t+2} = k | S_{t+1} = j,S_{t} = i)P(S_{t+1} = j|S_{t}=i)$

   이를 $Q$의 $i$번째 row와 $Q$의 $k$번째 column으로 나타내면 다음과 같다.

   > $\displaystyle\sum_{j \in S} q_{ij} \times q_{jk} = Q^{2}_{ik}$

   이를 일반화하면 다음과 같다.

   > $P(S_{t+n}=j|S_{t}=i) = Q^{n}_{ij} = [Q_{ij}]^{n}$

   따라서 $t+m$ 시점의 분포는 $\vec{v}Q^{n}$이 된다. Transition probability matrix은 markov process의 변화 추이를 나타내는 것이기 때문에, 현재 state의 분포 $v$에 변화 추이를 곱하면 미래를 예측할 수 있다. State가 $n$번 transition한 경우에는 $n$번 곱하여 구할 수 있다. 결과적으로 위의 수식과 동일하다.

6. stationary distribution

   만약 어떤 $\vec{v}Q^{n}$이 어떤 극한 분포에 수렴한다면, 이를 stationary distribution(정적 분포)이라고 한다. 이는 현재 state의 분포가 시간에 따라 변하지 않는 것을 의미한다. 이렇게 수렴하여 변하지 않는 상태를 stationary state(정상 상태)라고 한다.

   $\vec{v}Q^{n}$이 다음 조건을 만족한다면,

   > $\vec{v}Q = \vec{v}$

   이와 같이 정리할 수 있다.

   > $\vec{v}Q^n = \vec{v}Q^{n-1} \dots = \vec{v}Q^2 = \vec{v}Q = \vec{v}$

   행렬 $Q$를 linear transformation(선형 변환)으로 봤을 때, $Q$에 의한 변환이 자기 자신의 상수배가 되는 vector를 eigenvector라고 한다. 이때 상수를 eigenvalue라고 한다. 이를 식으로 표현하면 다음과 같다.

   > $Q\vec{v} = \lambda\vec{v}$

   $\lambda$는 행렬 $Q$의 eigenvalue이며, $\vec{v}$는 행렬 $Q$에 대한 eigenvector이다. 여기서는 stationary distribution이 eigenvector가 된다.

   따라서 stationary distribution은 $\lambda=1$에 대응하는 eigenvector가 된다. 즉, markov process의 transition probability matrix의 eigenvalue 중 하나는 반드시 1이여야 한다.

   Stationary distribution를 찾기 위해서는 transition probability matrix $Q$의 eigenvalue와 eigenvector를 구하면 된다. 이때 eigenvalue가 1인 eigenvector가 stationary distribution이 된다. 이를 구하는 과정은 다음과 같다.

   1. Transition probability matrix $Q$를 구한다.
   2. $Q$의 eigenvalue와 eigenvector를 구한다.
   3. Eigenvalue가 1인 eigenvector를 찾는다.
   4. Eigenvector를 정규화하여 stationary distribution를 구한다.

   예를 들어, 다음과 같은 transition probability matrix $Q$가 있다고 할 때,

   $$
   Q = \begin{pmatrix}
   0.5 & 0.5 \\
   0.2 & 0.8
   \end{pmatrix}
   $$

   이 행렬의 eigenvalue $\lambda$와 eigenvector $\vec{v}$를 구하면 다음과 같다.

   $$
   \lambda_1 = 1, \lambda_2 = 0.3 \\
   \vec{v_1} = \begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix}, \vec{v_2} = \begin{pmatrix} -0.8 \\ 0.6 \end{pmatrix}
   $$

   여기서 eigenvalue가 1인 eigenvector $\vec{v_1}$이 stationary distribution이 된다. 이를 정규화하면 다음과 같다.

   $$
   \vec{x} = \frac{1}{0.4 + 0.6} \begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix} = \begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix}
   $$

   따라서 stationary distribution는 $\begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix}$가 된다.

---

## Markov Reward Process

Markov process는 현재 state만이 다음 state를 결정하는 것이라면, Markov reward process는 현재 state와 다음 state의 보상을 고려하여 다음 state를 결정하는 것이다.
