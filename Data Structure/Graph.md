# 그래프

> Graph는 원소 사이의 다:다 관계를 표현하는 비선형 자료구조이다.

---

## 이해

1. 개념

   Graph는 각 객체를 vertex(정점)과 그를 연결하는 edge(간선)으로 표현하는 자료구조이다. 두 vertex를 연결하는 edge가 존재할 때, 그 두 vertex는 adjacent(인접)하다고 하고, 그 edge는 두 vertex에 incident(부속)되어 있다고 한다. 이렇게 **vertex에 incident된 edge의 수를 그 vertex의 degree(차수)**라고 한다.

2. 종류

   Graph는 그 방향성의 유무에 따라 다음 두 종류로 나뉜다.

   1. undirected(무방향) graph

      두 vertex를 연결하는 edge에 방향이 없는 graph이다.

      Vertex $V_i$와 $V_j$를 연결하는 edge는 $(V_i, V_j)$로 표현하고, $(V_j, V_i)$와도 같은 edge이다.

   2. directed(방향) graph

      두 vertex를 연결하는 edge에 방향이 있는 graph이며, digraph라고 하기도 한다.

      Vertex $V_i$에서 $V_j$로 가는 edge는 $<V_i, V_j>$로 표현하고, $V_j$에서 $V_i$로 가는 edge인 $<V_j, V_i>$와 다른 edge이다.

   Graph의 연결에 따라 다음과 같이 나뉠 수도 있다.

   1. complete(완전) graph

      Graph의 모든 vertex가 서로 연결되어 있어, 최대 edge 수를 가지는 graph이다. Directed graph의 경우 모든 방향에 대해 최대 edge 수를 가진다.

   2. subgraph

      원래 graph에서 vertex나 edge 일부를 제거하여 만든 graph를 subgraph라고 한다.

   3. weight(가중) graph

      각 edge에 가중치를 할당한 graph이다. Network라고 하기도 한다.

---
