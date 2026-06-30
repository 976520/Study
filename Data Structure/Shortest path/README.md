# shortest path

> Shortest path는 weight graph에서 어떠한 두 vertex 사이를 연결하는 path 중 edge weight의 총합이 최소인 path이다.

---

## 이해

Weight graph $G = (V, E)$에서 각 edge $(u, v)$는 weight $w(u, v)$를 가진다. 이때 vertex $u$에서 vertex $v$로 가는 여러 path 중에서 거쳐가는 edge들의 weight 총합이 가장 작은 path를 shortest path(최단 경로)라고 하고, 그 weight의 총합을 distance(거리)라고 한다.

최단 경로를 구할 때 주의할 점은 negative weight(음의 가중치)와 negative cycle(음의 사이클)이다. Edge weight가 음수일 수 있으면 단순히 가까운 vertex부터 확정하는 방법이 성립하지 않고, cycle을 돌수록 distance가 무한히 감소하는 negative cycle이 존재하면 최단 경로 자체가 정의되지 않는다.

---

## 종류

무엇을 구하느냐에 따라 다음과 같이 나뉜다.

1. single source shortest path(단일 출발점 최단 경로)

   > 하나의 시작 vertex에서 다른 모든 vertex까지의 최단 경로를 구하는 방식이다.

   [Dijkstra](https://github.com/976520/Study/blob/main/Data%20Structure/Shortest%20path/Dijkstra.md)

   [Bellman-Ford](https://github.com/976520/Study/blob/main/Data%20Structure/Shortest%20path/Bellman-Ford.md)

2. single pair shortest path(단일 쌍 최단 경로)

   > 특정한 두 vertex 사이의 최단 경로만을, 목적지를 향한 방향성을 이용하여 구하는 방식이다.

   [A\*](https://github.com/976520/Study/blob/main/Data%20Structure/Shortest%20path/A-star.md)

3. all pairs shortest path(모든 쌍 최단 경로)

   > 모든 vertex 쌍에 대해 서로 간의 최단 경로를 구하는 방식이다.

   [Floyd-Warshall](https://github.com/976520/Study/blob/main/Data%20Structure/Shortest%20path/Floyd-Warshall.md)

---

## 비교

| algorithm | 문제 | 음의 가중치 | 시간 복잡도 |
| --- | --- | --- | --- |
| dijkstra | single source | 불가 | $O((V + E)\log V)$ |
| bellman-ford | single source | 가능 | $O(VE)$ |
| floyd-warshall | all pairs | 가능 | $O(V^3)$ |
| A\* | single pair | 불가 | $O(E)$ (heuristic에 의존) |
