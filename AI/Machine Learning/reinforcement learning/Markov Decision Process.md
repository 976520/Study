# Markov Decision Process

> Markov decision process는 discrete time stochastic control process(이산 시간 확률 제어 과정)이다.

~~수학이 싫은 강화학습 엔지니어 꿈나무들은 도망가주시기 바랍니다.~~

---

## Stochastic process

1. 이해

   > Stochastic process(확률 과정)는 시간의 진행에 대해 확률적인 변화를 가지는 구조를 의미한다.

   쉽게 설명하면, 시간에 따라 일어나는 일들이 확률에 따라 결정되는 과정이다. 이때 시간은 연속적이거나 이산적일 수 있다.

   예를 들어, 날씨를 stochastic process로 modeling한다고 할 때, 날씨의 state는 "맑음", "흐림", "비"의 세 가지로 정의할 수 있다. 각 state에서 다른 state로 바뀔 확률이 다음과 같다고 가정하면,

   - "맑음" => "맑음" 일 확률: 0.7
   - "맑음" => "흐림" 일 확률: 0.2
   - "맑음" => "비" 일 확률: 0.1

   - "흐림" => "맑음" 일 확률: 0.4
   - "흐림" => "흐림" 일 확률: 0.4
   - "흐림" => "비" 일 확률: 0.2

   - "비" => "맑음" 일 확률: 0.3
   - "비" => "흐림" 일 확률: 0.5
   - "비" => "비" 일 확률: 0.2

   이 예시에서 각 상태에서 변경될 수 있는 모든 확률의 합은 1이 된다. 예를 들어 "맑음" 상태에서 "맑음", "흐림", "비"로 변경될 확률의 합은 0.7 + 0.2 + 0.1 = 1이다.

2. State transition probability

   Stochastic process에서 시간 $t$에 따른 state $S_{t}$의 변화를 나타내고, 이 상태의 변화를 transition(전이)이라고 한다. 이러한 변화를 확률로 표현하면 state transition probability(상태 전이 확률)이라고 한다.

   $t$에서의 상태를 $i$라고 하고, $t+1$에서의 상태를 $j$라고 하면, $i$에서 $j$로 이동할 확률 state transition probability $P_{ij}$는 conditional probability(조건부 확률)를 이용해 다음과 같이 나타낼 수 있다.

   $$P_{ij} = P(S_{t+1} = j | S_{t} = i)$$

   이에 대한 조건은 다음과 같다.

   1. 상태 $i$에서 상태 $j$로 transition할 probability가 존재한다.

      $$P_{ij}>0$$

   2. 상태 $i$에서 가능한 모든 $j$로의 transition probability의 합은 1이다.

      $$\sum_{j \in S} P_{ij} = 1$$

      즉, 상태 $i$에서 반드시 어떤 상태 $j$로 transition하게 된다.

3. State transition diagram

   State transition diagram은 environment의 모든 state와 state transition probability를 나타낸 directed cyclic graph이다.

   <img src="https://github.com/user-attachments/assets/64d2ec4f-2564-4191-b2fe-567a06bb4f98" width="500">

   위 transition diagram에서는 각 node가 state $s$를 나타내고, edge는 state transition을 의미하며, edge의 숫자로 state transition probability $P_{ss'}$를 나타낸다.

   `독서`에서 `웹 서핑`, `취침`으로 이동할 확률을 모두 더하면 1이 나온다. 이처럼 하나의 state에서 다른 state로 이동할 확률의 총합은 1인 것을 알 수 있다. 그리고 `취침`은 종료 state이기 때문에 다른 state로 이동할 확률은 0이며, 동시에 자신의 상태를 유지할 확률이 1이다.

4. State vector

   > State vector는 현재 시점에서 각 state에 있을 확률을 나타낸 vector이다.

   State vector는 현재 시점 $t$에서의 상태 분포를 나타내며, 각 element는 해당 state에 있을 확률을 나타낸다. 예를 들어, 현재 시점 $t$에서의 state vector $\vec{v}$가 다음과 같다고 할 때.

   $$
   \vec{v} = \begin{bmatrix}
   0.2 \\
   0.3 \\
   0.1 \\
   0.4 \\
   0
   \end{bmatrix}
   $$

   이 vector는 현재 시점 $t$에서 첫 번째 state에 있을 확률이 20%, 두 번째 state에 있을 확률이 30%, 세 번째 state에 있을 확률이 10%, 네 번째 state에 있을 확률이 40%, 다섯 번째 state에 있을 확률이 0%임을 나타낸다. 모든 확률의 합이 100%가 되어야 하므로, state vector의 각 element의 합은 1이다.

   State vector는 시간에 따라 변화하며, 후술할 state transition probability matrix와의 행렬곱을 통해 다음 시점의 state vector를 구할 수 있다. 현재 시점 $t$의 state vector $\vec{v}$와 state transition probability matrix $Q$가 주어졌을 때, 다음 시점 $t+1$의 state vector $\vec{v}'$는 다음과 같다.

   $$
   \vec{v}' = \vec{v}Q
   $$

5. State transition probability matrix

   > State transition probability matrix는 모든 state의 전이 확률을 나타낸 행렬이다.

   State transition probability matrix는 전체 markov process의 각 state가 다른 state로 변화 추이를 나타낸다.

   State transition diagram를 행렬로 표현한 것이다. 모든 element가 0 이상 1 이하의 값을 가지며 각 row의 합이 1인 것(row stochastic)을 확인할 수 있다. 위의 예시 transition diagram에 대한 state transition probability matrix는 다음과 같다.

   $$
   Q = \begin{bmatrix}
   0 & 0.1 & 0.1 & 0.8 & 0 \\
   0 & 0 & 0.3 & 0 & 0.7 \\
   0.1 & 0.2 & 0.2 & 0 & 0.5 \\
   0.6 & 0 & 0 & 0.4 & 0 \\
   0 & 0 & 0 & 0 & 1 \\
   \end{bmatrix}
   $$

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

---

## Markov process

> Markov process는 markov property를 가진 stochastic process이다.

정의된 확률 분포를 따라 state 사이를 이동하는 과정이다.

1. Markov property

   Markov process는 어떤 state가 연속 시간에서(in continuous time) 변화하고, 다음 state $S_{t+1}$가 현재 state $S_{t}$에만 의존하여 확률적으로 변화하는 것을 뜻한다. 즉, $S_{t+1}$에는 $S_{t}$만이 영향을 미칠 수 있으며, 그 이전 history는 영향을 미치지 않는다. 때문에 과거와 현재의 state를 모두 고려 했을 때 미래의 state가 나타날 확률과 현재의 state만 고려했을 때 미래의 state가 나타날 확률이 동일하다. 이를 수식으로 나타내면 다음과 같다.

   $$P(S_{t+1} | S_{t}) = P(S_{t+1} | S_{t}, ..., S_{t-1}, S_{t})$$

   이러한 성질을 markov property라고 한다. **Markov property은 $S_{t}$가 $S_{t+1}$를 결정하는 데 필요한 모든 정보를 포함하고 있다는 것**을 의미한다. 따라서 과거의 상태는 현재의 상태를 통해 간접적으로만 영향을 미치게 된다.

2. Markov chain

   > Markov chain은 markov property를 가진 discrete time stochastic process(이산 시간 확률 과정)이다.

   Markov process중 이산 시간에서(in discrete time) 동작하는 model을 Markov chain이라고 한다. 시간이 불연속적, 즉 단계별(step-by-step)로 변화한다. State는 이산적이며 일반적으로 정수로 표현된다. 각 단계에서 가능한 state의 수는 유한하거나 무한하다.

3. Irreducible

   Irreducible한 markov process는 모든 state가 서로 도달 가능한 state임을 의미한다. 즉, 임의의 state $i$에서 다른 임의의 state $j$로 도달할 수 있는 경로가 존재한다면, 그 markov process은 irreducible이라고 한다.

   이를 수식으로 나타내면 다음과 같다.

   상태 $i$에서 상태 $j$로 도달할 수 있는 확률을 $P_{ij}^{(n)}$라고 할 때, 어떤 양의 정수 $n$에 대해 다음이 성립하면,

   $$P_{ij}^{(n)} > 0$$

   상태 $i$에서 상태 $j$로 도달할 수 있다고 한다. 모든 상태 쌍 $(i, j)$에 대해 이러한 조건이 성립하면, 그 markov process은 irreducible이다.

   Irreducible markov process는 모든 상태가 서로 연결되어 있어, 시스템이 어느 상태에서 시작하더라도 결국 모든 상태를 방문할 수 있음을 보장한다.

4. State transition probability matrix를 이용한 state 예측

   State transition probability matrix와 현재 state를 알고 있다면 행렬곱을 이용하여 전체 process의 state를 구할 수 있다. 현재 시점 $t$에 대한 state $S_t$가 $(1\times M)$ 행렬로 표현된 state vector $\vec{v}$를 따를 때,

   $$P(S_{t+1} = j) = \displaystyle\sum_{i \in S} P(S_{t+1} = j | S_t = i)P(S_t = i)$$

   이는 내적을 이용하여 다음과 같이 나타낼 수 있다.

   $$\displaystyle\sum_{i \in S} v_{i}\times{q}_{ij}=\vec{v}Q$$

   이때 $v_i$는 $(1\times M)$ 행렬이고, $q_{ij}$는 $(M\times M)$ 정방행렬이다. 따라서 $t+1$ 시점의 transition probability matrix는 $(1\times M)$의 $\vec{v}Q$가 된다.

   $t+2$ 시점의 경우에는 다음과 같은데,

   $$P(S_{t+2} = k|S_{t} = i) = \displaystyle\sum_{j \in S} P(S_{t+2} = k | S_{t+1} = j,S_{t} = i)P(S_{t+1} = j|S_{t}=i)$$

   이를 $Q$의 $i$번째 row와 $Q$의 $k$번째 column으로 나타내면 다음과 같다.

   $$\displaystyle\sum_{j \in S} q_{ij} \times q_{jk} = Q^{2}_{ik}$$

   이를 일반화하면 다음과 같다.

   $$P(S_{t+n}=j|S_{t}=i)=Q^{n}_{ij} = [Q_{ij}]^{n}$$

   따라서 $t+m$ 시점의 분포는 $\vec{v}Q^{n}$이 된다. Transition probability matrix은 markov process의 변화 추이를 나타내는 것이기 때문에, 현재 state의 분포 $v$에 변화 추이를 곱하면 미래를 예측할 수 있다. State가 $n$번 transition한 경우에는 $n$번 곱하여 구할 수 있다. 결과적으로 위의 수식과 동일하다.

   예를 들어, 현재 state vector $\vec{v}$와 state transition probability matrix $Q$가 다음과 같다고 가정하면,

   $$
   \vec{v} = \begin{bmatrix}
   0.2 & 0.3 & 0.1 & 0.4 & 0
   \end{bmatrix}
   $$

   $$
   Q = \begin{bmatrix}
   0 & 0.1 & 0.1 & 0.8 & 0 \\
   0 & 0 & 0.3 & 0 & 0.7 \\
   0.1 & 0.2 & 0.2 & 0 & 0.5 \\
   0.6 & 0 & 0 & 0.4 & 0 \\
   0 & 0 & 0 & 0 & 1 \\
   \end{bmatrix}
   $$

   ```python
   v = np.array([0.2, 0.3, 0.1, 0.4, 0])

   Q = np.array([
       [0, 0.1, 0.1, 0.8, 0],
       [0, 0, 0.3, 0, 0.7],
       [0.1, 0.2, 0.2, 0, 0.5],
       [0.6, 0, 0, 0.4, 0],
       [0, 0, 0, 0, 1]
   ])
   ```

   이때 $t+1$ 시점의 state vector는 다음과 같이 구할 수 있다.

   $$
   \vec{v}Q = \begin{bmatrix}
   0.2 & 0.3 & 0.1 & 0.4 & 0
   \end{bmatrix}
   \begin{bmatrix}
   0 & 0.1 & 0.1 & 0.8 & 0 \\
   0 & 0 & 0.3 & 0 & 0.7 \\
   0.1 & 0.2 & 0.2 & 0 & 0.5 \\
   0.6 & 0 & 0 & 0.4 & 0 \\
   0 & 0 & 0 & 0 & 1 \\
   \end{bmatrix}
   = \begin{bmatrix}
   0.26 & 0.08 & 0.17 & 0.32 & 0.17
   \end{bmatrix}
   $$

   ```python
   v_next = np.dot(v, Q)
   ```

   따라서 $t+1$ 시점의 state vector는 $\begin{bmatrix} 0.26 & 0.08 & 0.17 & 0.32 & 0.17 \end{bmatrix}$가 된다.

   ```python
   print(v_next) # 출력: [0.26 0.08 0.17 0.32 0.17]
   ```

   이와 같이 state vector와 transition matrix의 행렬곱을 이용하여 markov process의 미래 상태를 예측할 수 있다.

5. Identity Matrix

   > Identity matrix는 대각선 요소가 모두 1이고 나머지 요소가 모두 0인 정방 행렬이다.

   Identity matrix는 행렬 곱셈에서 항등원 역할을 한다. 즉, 어떤 행렬 $A$에 대해 $A$와 identity matrix $I$를 곱하면 $A$가 그대로 나온다. 이를 수식으로 나타내면 다음과 같다.

   $$
   AI = IA = A
   $$

   Identity matrix는 markov process의 state transition probability matrix에서 각 상태가 자기 자신으로 전이될 확률이 1인 경우를 나타낸다. 즉, 모든 상태가 변하지 않고 그대로 유지되는 경우를 의미한다. 예를 들어, 다음과 같은 3x3 identity matrix $I$가 있다고 하자.

   $$
   I = \begin{bmatrix}
   1 & 0 & 0 \\
   0 & 1 & 0 \\
   0 & 0 & 1
   \end{bmatrix}
   $$

   이 identity matrix를 어떤 행렬 $A$와 곱하면 $A$가 그대로 나온다.

   $$
   A = \begin{bmatrix}
   a & b & c \\
   d & e & f \\
   g & h & i
   \end{bmatrix}
   $$

   $$
   AI = \begin{bmatrix}
   a & b & c \\
   d & e & f \\
   g & h & i
   \end{bmatrix}
   \begin{bmatrix}
   1 & 0 & 0 \\
   0 & 1 & 0 \\
   0 & 0 & 1
   \end{bmatrix}
   = \begin{bmatrix}
   a & b & c \\
   d & e & f \\
   g & h & i
   \end{bmatrix}
   $$

   이처럼 identity matrix는 행렬 곱셈에서 항등원 역할을 하며, markov process에서는 상태가 변하지 않는 경우를 나타낸다. 행렬의 크기에 따라 다양한 크기의 identity matrix가 존재한다.

6. Stationary distribution

   만약 어떤 $\vec{v}Q^{n}$이 어떤 극한 분포에 수렴한다면, 이를 stationary distribution(정적 분포)이라고 한다. 이는 현재 state의 분포가 시간에 따라 변하지 않는 것을 의미한다. 이렇게 수렴하여 변하지 않는 상태를 stationary state(정상 상태)라고 한다.

   $\vec{v}Q^{n}$이 다음 조건을 만족한다면,

   $$\vec{v}Q = \vec{v}$$

   이와 같이 정리할 수 있다.

   $$\vec{v}Q^n = \vec{v}Q^{n-1} \dots = \vec{v}Q^2 = \vec{v}Q = \vec{v}$$

   이때 $Q$가 identity matrix라고 할 수 있으며, 이때의 분포가 stationary distribution이 된다.

   행렬 $Q$를 linear transformation(선형 변환)으로 봤을 때, $Q$에 의한 변환이 자기 자신의 상수배가 되는 vector를 eigenvector라고 한다. 이때 상수를 eigenvalue라고 한다. 이를 식으로 표현하면 다음과 같다.

   $$Q\vec{v} = \lambda\vec{v}$$

   $\lambda$는 행렬 $Q$의 eigenvalue이며, $\vec{v}$는 행렬 $Q$에 대한 eigenvector이다. 여기서는 stationary distribution이 eigenvector가 된다.

   따라서 stationary distribution은 $\lambda=1$에 대응하는 eigenvector가 된다. 즉, markov process의 transition probability matrix의 eigenvalue 중 하나는 반드시 1이여야 한다.

   이를 통해 stationary distribution를 찾을 수 있다. 간단히 transition probability matrix $Q$의 eigenvalue와 eigenvector를 구하고, eigenvalue가 1인 eigenvector가 stationary distribution을 찾으면 된다. 이 과정을 예시로 설명하자면 다음과 같다.

   다음과 같은 transition probability matrix $Q$가 있다고 할 때,

   $$
   Q = \begin{pmatrix}
   0.5 & 0.5 \\
   0.2 & 0.8
   \end{pmatrix}
   $$

   ```python
   Q = np.array([[0.5, 0.5],
                 [0.2, 0.8]])
   ```

   이 행렬의 eigenvalue $\lambda$와 eigenvector $\vec{v}$를 구하면 다음과 같다.

   $$
   \lambda_1 = 1, \lambda_2 = 0.3 \\
   \vec{v_1} = \begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix}, \vec{v_2} = \begin{pmatrix} -0.8 \\ 0.6 \end{pmatrix}
   $$

   ```python
   eigenvalues, eigenvectors = np.linalg.eig(Q)
   ```

   여기서 eigenvalue가 1인 eigenvector $\vec{v_1}$이 stationary distribution이 된다.

   ```python
   stationary_vector = eigenvectors[:, np.isclose(eigenvalues, 1)]
   ```

   이를 정규화하면 다음과 같다.

   $$
   \vec{x} = \frac{1}{0.4 + 0.6} \begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix} = \begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix}
   $$

   ```python
   stationary_distribution = stationary_vector / np.sum(stationary_vector)
   ```

   따라서 stationary distribution는 $\begin{pmatrix} 0.4 \\ 0.6 \end{pmatrix}$가 된다.

   ```python
   print(stationary_distribution) # 출력: [0.4 0.6]
   ```

   만약 행렬 $Q$가 전치 행렬 $Q^T$를 가지고 있다면, 이를 이용하여 stationary distribution를 찾을 수 있다. 예를 들어, 다음과 같은 행렬 $Q$가 있다고 할 때,

   $$
   Q^T = \begin{pmatrix}
   0.5 & 0.2 \\
   0.5 & 0.8
   \end{pmatrix}
   $$

   ```python
   Q_T = Q.T
   ```

   이 전치 행렬의 eigenvalue $\lambda$와 eigenvector $\vec{v}$를 구하면 다음과 같다.

   $$
   \lambda_1 = 1, \lambda_2 = 0.3 \\
   \vec{v_1} = \begin{pmatrix} 0.6 \\ 0.4 \end{pmatrix}, \vec{v_2} = \begin{pmatrix} 0.6 \\ -0.8 \end{pmatrix}
   $$

   ```python
   eigenvalues_T, eigenvectors_T = np.linalg.eig(Q_T)
   ```

   여기서 eigenvalue가 1인 eigenvector $\vec{v_1}$이 stationary distribution이 된다.

   ```python
   stationary_vector_T = eigenvectors_T[:, np.isclose(eigenvalues_T, 1)]
   ```

   이를 정규화하면 다음과 같다.

   $$
   \vec{x} = \frac{1}{0.6 + 0.4} \begin{pmatrix} 0.6 \\ 0.4 \end{pmatrix} = \begin{pmatrix} 0.6 \\ 0.4 \end{pmatrix}
   $$

   ```python
   stationary_distribution_T = stationary_vector_T / np.sum(stationary_vector_T)
   ```

   따라서 stationary distribution는 $\begin{pmatrix} 0.6 \\ 0.4 \end{pmatrix}$가 된다.

   ```python
   print(stationary_distribution_T) # 출력: [0.6 0.4]
   ```

   원래 행렬 $Q$의 stationary distribution에 전치를 취한 것과 같다는 점을 확인할 수 있다.

   ```python
   print(stationary_distribution_T == stationary_distribution.T) # 출력: True
   ```

---

## Markov Reward Process

1. 이해

   > Markov reward process는 markov process에 reward system을 추가한 것이다.

   Markov process는 현재 state만이 다음 state를 결정하는 것이라면, Markov reward process는 현재 state와 **다음 state의 reward를 고려**하여 다음 state를 결정하는 것이다. 여기서 reward는 현재 state에서 다음 state로 transition할 때 이동한 미래 state의 좋고 나쁨에 따라 현재 state에 부여하는 보상을 의미한다.

2. return function

   1. 이해

      시점 $t$에서 return은 episode의 모든 기간에 걸쳐 얻은 reward의 총합이다. $R_{t+1}=r$이 $t$에서 action을 수행한 후 얻은 즉각적인 reword이라고 할 때, 다음으로 이어지는 reword은 $R_{t+2}, R_{t+3}, \cdots$이다. 이러한 reword들을 모두 더하면 시점 $t$에서의 return이 된다.

      $$
      G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \cdots = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}
      $$

      여기서 $\gamma$는 discount factor이다. 이 값은 0보다 크고 1보다 작으며, 현재 시점에서 미래 reword이 얼마나 가치 있는지 나타낸다. $\gamma=0$이면, 미래 reword를 고려하지 않는다는 의미이고, $\gamma=1$이면, return은 모든 미래의 reward를 그대로 모두 더한 값이 된다.

   2. return function의 재귀적 표현

      이 return function을 재귀적으로 표현하여 다음과 같이 쓸 수 있다.

      $$
      G_t = R_{t+1}+\gamma G_{t+1} = r + \gamma G_{t+1}
      $$

      이는 시점 t에서 return이 즉각적인 보상 $r$과 다음 시점 $t+1$에서 discount factor이 적용된 미래의 return을 더한 것이라는 의미이다.

3. policy function

   1. 이해

      Policy는 다음에 선택할 action을 결정하는 함수이다. 이는 결정적일 수도 있고, 확률적일 수도 있다는 특징이 있다. 확률적 policy는 주어진 state에서 agent가 선택할 수 있는 action에 대한 확률 분포를 가진다.

      $$
      \pi(a|s)=P[A_t=a|S_t=s]
      $$

   2. optimal policy

      학습 중에 agent가 더 많은 경험을 얻으면 policy가 바뀔 수 있다. 만약 처음에 agent가 모든 action의 확률이 균등한 policy로 시작했다면, agent는 optimal policy에 가깝게 되도록 학습을 할 것이다. 이때 optimal policy는 가장 높은 return을 만드는 policy로, $\pi^*(a|s)$로 표현한다.

4. state-value function

   강화학습에서 agent는 reword를 많이 받는 행동을 선택하도록 학습한다. 보상은 action을 수행한 후 다음 state에서 제공되므로, 이처럼 받지 않은 reword를 고려해야 한다.

   State value function은 특정 상태가 궁극적인 목표를 달성하는데 있어서 얼마나 좋은지 나쁜지를 측정하는 척도이다. 이는 return을 기준으로 한다.

   상태 $s$의 value function을 policy $\pi$를 따른 후 모든 episode에 걸친 평균 return $G_t$의 기댓값 $v_\pi(s)$는 다음과 같다.

   $$
   v_\pi(s) = E_\pi[G_t|S_t=s]=E_\pi[\displaystyle\sum_{k=0}^{\infty}\gamma^k R_{t+k+1}|S_t=s]
   $$

   현재 state에서 한 episode가 끝날 때까지 받은 reword의 합을 통해 현재 state의 value를 측정할 수 있다. 하지만 reword의 단순 합으로 value function을 작성하면 시간 개념을 적용할 수 없다는 단점이 있다. 따라서 discount factor $\gamma$를 곱해 미래의 reword를 discount하여 return을 구하는 것이다. Reword가 확률변수임에 따라 return도 확률변수이기 때문에 평균을 의미하는 기댓값을 취하여 value function을 유도하는 것이다.

5. bellman equation

   $v_\pi(s)$는 다음과 같이 재귀적으로 표현할 수 있으며,

   $$
   v_\pi(s) = E_\pi[R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}+\cdots|S_t=s] = E_\pi[R_{t+1}+\gamma v_{\pi}(S_{t+1})|S_t=s]
   $$

   $$
   v_\pi(s) = \sum_{a\in A}\pi(a|s)\sum_{s'\in S}p(s'|s,a)[R(s,a,s')+\gamma v_\pi(s')]
   $$

   이를 bellman equation이라고 한다. 이 방정식은 현재 상태의 가치를 immediate(즉각적) reward $R(s,a,s')$과 다음 상태의 discounted(할인된) value $\gamma v_\pi(s')$의 합으로 표현한다.

6. action-value function

   State-value function을 통해 다음 state들의 value를 판단할 수 있으며, agent는 이를 바탕으로 더 value가 높은 state로 가기 위한 action을 선택하여 state를 transition하게 된다.

   하지만 여기서 다음과 같은 문제가 발생한다.

   1. Agent가 다음에 도달할 수 있는 모든 state들의 정보를 미리 알고 있어야 한다.

   2. 특정 action을 선택하더라도 원하는 state로 항상 이동할 수 있다는 보장이 없다. 즉, state transition probability를 고려해야 한다.

   때문에 action에 대한 value function이 필요하다. Action-value function은 state-action pair에 대해 value를 정의한 것으로, 특정 state에서 취한 action이 얼마나 좋을 지 판단하는 것이다.

   상태 $s$에서 선택한 행동 $a$에 대한 return $G_t$의 기댓값 $q_\pi(s,a)$는 다음과 같다.

   $$
   q_\pi(s,a) = E_\pi[G_t|S_t=s,A_t=a] = E_\pi[\displaystyle\sum_{k=0}^{\infty}\gamma^k R_{t+k+1}|S_t=s,A_t=a]
   $$

---

## Markov Decision Process

> Markov decision process는 markov reward process에 action을 추가한 것이다.

일반적으로 강화학습이 다루는 문제라고 할 수 있다. 이 Markov decision process를 푸는 방법으로 Dynamic Programming, Monte Carlo method, Temporal Difference Learning(시간 차 학습) 등이 있다.

---
