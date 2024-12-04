# 그래프

> Graph는 원소 사이의 다:다 관계를 표현하는 비선형 자료구조이다.

---

## 이해

Graph는 각 객체를 vertex(정점)과 그를 연결하는 edge(간선)으로 표현하는 자료구조이다. 두 vertex를 연결하는 edge가 존재할 때, 그 두 vertex는 adjacent(인접)하다고 하고, 그 edge는 두 vertex에 incident(부속)되어 있다고 한다. 이렇게 **vertex에 incident된 edge의 수를 그 vertex의 degree(차수)**라고 한다.

Graph는 그 방향성의 유무에 따라 다음 두 종류로 나뉜다.

1.  undirected(무방향) graph

    두 vertex를 연결하는 edge에 방향이 없는 graph이다.

    Vertex $V_i$와 $V_j$를 연결하는 edge는 $(V_i, V_j)$로 표현하고, $(V_j, V_i)$와도 같은 edge이다.

2.  directed(방향) graph

    두 vertex를 연결하는 edge에 방향이 있는 graph이며, digraph라고 하기도 한다.

    Vertex $V_i$에서 $V_j$로 가는 edge는 $<V_i, V_j>$로 표현하고, $V_j$에서 $V_i$로 가는 edge인 $<V_j, V_i>$와 다른 edge이다.

Graph의 연결에 따라 다음과 같이 나뉠 수도 있다.

3.  complete(완전) graph

    Graph의 모든 vertex가 서로 연결되어 있어, 최대 edge 수를 가지는 graph이다. Directed graph의 경우 모든 방향에 대해 최대 edge 수를 가진다.

4.  subgraph

    원래 graph에서 vertex나 edge 일부를 제거하여 만든 graph를 subgraph라고 한다.

5.  weight(가중) graph

    각 edge에 가중치를 할당한 graph이다. Network라고 하기도 한다.

## traversal

한 vertex에서 시작하여 연결된 모든 vertex를 방문하는 것을 graph의 traversal(순회)이라고 한다.

1. depth-first search(깊이 우선 탐색)

   한 우물만 깊게 판다고 생각하면 된다.

   시작 vertex에서 경로가 끝날 때까지 한 방향으로 탐색한다. 더 이상 갈 곳이 없으면, 가장 마지막에 있었던 갈림길로 돌아와 다른 방향으로 탐색한다. 갈림길 vertex로 돌아가서 다시 탐색을 해야 하기 때문에 **stack**을 사용하여 구현할 수 있다.

   1. 시작 vertex $V_0$을 설정하고 방문한다.

   2. $V_0$에 인접한 vertex 중에서 방문하지 않은 정점 $V_1$을 방문하고 stack에 push하고 $V_1$을 $V_0$으로 설정하여 반복한다.

      만약 $V_0$에 인접한 vertex 중에서 방문하지 않은 정점이 없다면 stack을 pop하여 가장 마지막에 방문한 정점을 $V_0$으로 설정하고 반복한다.

   3. stack이 공백이 될 때까지 반복한다.

2. breadth-first search(너비 우선 탐색)

   여러 우물을 골고루 판다고 생각하면 된다. Queue 자료구조를 사용한다.

   시작 vertex에서 인접한 모든 vertex를 방문하고, 방문했던 vertex에서 다시 인접한 모든 vertex를 방문하는 방식으로 순회한다. 인접한 vertex를 차례로 다시 탐색을 해야 하기 때문에 방문한 vertex를 순서대로 저장하는 **queue**를 사용한다.

   1. 시작 vertex $V_0$을 설정하고 방문한다.

   2. $V_0$에 인접한 vertex 중에서 방문하지 않은 정점 $V_1$을 방문하며 enQueue하고, $V_1$을 $V_0$으로 설정하여 반복한다.

      $V_0$에 인접한 vertex 중에서 방문하지 않은 정점이 없다면 deQueue하여 받은 vertex를 $V_0$으로 설정하고 반복한다.

   3. queue가 공백이 될 때까지 반복한다.

---
