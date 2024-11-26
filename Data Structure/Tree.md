# 나무

> Tree는 비선형이자 계층형(hierarchial) 자료구조이다.

---

## 이해

<img src="https://github.com/user-attachments/assets/c9339bd1-6b99-4f96-bcdb-e697d8f9b8ce" height="300"/>

Tree를 구성하는 각 원소를 node라고 하고, 부모 node와 자식 node를 연결하는 선을 edge라고 한다. Tree의 계층을 하는 level이라는 개념이 있다.

Tree의 시작이 되는 최상위 node를 root node라고 하며, 이는 level 0이다. 자식 node가 없는 최하위 node를 leaf node 또는 terminal(단말) node라고 한다. 단말 node가 아닌 degree가 1 이상인 node는 internal(내부) node라고 한다.

Subtree는 특정 node를 root로 하는 작은 tree를 의미한다. 위 그림에서 `2`는 `7`, `5`를 root로 하는 두 개의 subtree를 가지고 있다. 한 node가 가진 subtree의 수를 그 node의 degree(차수)라고 한다. Tree의 node 중 가장 높은 degree를 가지는 node의 degree가 그 tree의 degree가 된다.

여러 tree가 모인 집합을 forest라고 한다.

---
