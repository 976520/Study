# 나무

> Tree는 비선형이자 계층형(hierarchial) 자료구조이다.

---

## 이해

<img src="https://github.com/user-attachments/assets/c9339bd1-6b99-4f96-bcdb-e697d8f9b8ce" height="300"/>

Tree를 구성하는 각 원소를 node라고 하고, 부모 node와 자식 node를 연결하는 선을 edge라고 한다. Tree의 계층을 하는 level이라는 개념이 있다.

Tree의 시작이 되는 최상위 node를 root node라고 하며, 이는 level 0이다. 자식 node가 없는 최하위 node를 leaf node 또는 terminal(단말) node라고 한다. 단말 node가 아닌 degree가 1 이상인 node는 internal(내부) node라고 한다.

Subtree는 특정 node를 root로 하는 작은 tree를 의미한다. 위 그림에서 `2`는 `7`, `5`를 root로 하는 두 개의 subtree를 가지고 있다. 한 node가 가진 subtree의 수를 그 node의 degree(차수)라고 한다. Tree의 node 중 가장 높은 degree를 가지는 node의 degree가 그 tree의 degree가 된다.

Tree의 depth(깊이)는 자신을 제외한 모든 부모 node의 개수이다. 위 그림에서 `10`의 depth는 2이다. Root node의 depth는 0이다.

여러 tree가 모인 집합을 forest라고 한다.

---

## Binary tree

1. 이해

   > Tree의 모든 node의 degree가 2 이하인 tree이다.

   Binary tree는 좌우가 구분된 자식 node를 두 개만 가질 수 있으며, 이는 공백 node도 포함한다. 이때 왼쪽 자식 node를 left child, 오른쪽 자식 node를 right child라고 한다. 따라서 **binary tree의 모든 node는 left child와 right child를 root node로 하는 두 개의 subtree**를 가진다. 각 subtree도 모두 binary tree인 recursive 구조를 가진다.

2. 종류

     <img src="https://github.com/user-attachments/assets/0bf64ffe-ae3b-48ca-a379-5f93f98da7e6" height="300"/>

   1. 편향 binary tree

      모든 node가 왼쪽 혹은 오른쪽 자식 node만 가지는 tree이다.

   2. Complete(완전) binary tree

      처음부터 차근차근 채우는 tree이다.

   3. Full(포화) binary tree

      각 level이 모두 꽉 차있는 complete binary tree의 일종이다. 따라서 높이가 $h$인 full binary tree의 최대 node 개수는 $2^{h+1}-1$개이다.

3. 특징

   1. node의 개수가 $n$인 binary tree의 edge 개수는 $n-1$개이다.

      Root node를 제외한 모든 node는 하나의 edge를 가지므로, 모든 node의 edge 개수는 $n-1$개이다.

   2. 높이가 $h$인 binary tree의 최대 node 개수는 $2^{h+1}-1$개이다.

      하나의 node가 가질 수 있는 최대 자식 node 개수는 2개이므로, $i$번째 level의 최대 node 개수는 $2^i$개이다. 따라서 높이가 $h$인 binary tree의 최대 node 개수는 $2^0+2^1+2^2+...+2^h$이므로, $\displaystyle\sum^h_{i=0}2^i=2^{h+1}-1$개이다.

   3. 높이가 $h$인 binary tree의 최소 node 개수는 $h+1$개이다.

      편향 binary tree인 경우이다.

4. 구현

   1. 순차 자료구조에서 구현

      걍 순서대로 index 부여 해서 array로 쭉 나열하는 방법인데, 구현의 편의를 위해 0번 index는 비워두는 경우가 많다.

      Binary tree의 1차원 배열에서의 index는 다음과 같다.

      1. node $i$의 부모 node

         $[\frac{i}{2}]$

         이때 $[x]$는 $x$를 넘지 않는 최대 정수이다. 또한 $i$는 1보다 커야 한다. 첫 번째 node는 root node이므로 부모가 없다.

      2. node $i$의 left child

         $2i$

      3. node $i$의 right child

         $2i+1$

      4. root node

         $1$

   2. 연결 자료구조에서 binary tree 구현

      Data와 두 개의 pointer를 가진 link node를 사용한 node 구조체를 정의하여 사용하는 방법이다.

      ```c
      typedef struct TreeNode {
        char data;
        struct TreeNode *left, *right;
      } TreeNode;
      ```

      구조체를 사용하여 각 node를 정의하고,

      ```c
      TreeNode *root = NULL;
      TreeNode rootNode = {'A', NULL, NULL};
      TreeNode leftNode = {'B', NULL, NULL};
      TreeNode rightNode = {'C', NULL, NULL};
      ```

      각 node를 연결하여 tree를 구성한다.

      ```c
      root = &rootNode;
      rootNode.left = &leftNode;
      rootNode.right = &rightNode;
      ```

      이는 root node가 `A`이고, left child가 `B`, right child가 `C`인 tree가 된다.

      ```c
      printf("%c\n", root->data); // 출력: A
      printf("%c\n", root->left->data); // 출력: B
      printf("%c\n", root->right->data); // 출력: C
      ```

---
