# 나무

> Tree는 비선형이자 계층형(hierarchial) 자료구조이다.

---

## 이해

<img src="https://github.com/user-attachments/assets/c9339bd1-6b99-4f96-bcdb-e697d8f9b8ce" height="300"/>

Tree를 구성하는 각 원소를 node라고 하고, 부모 node와 자식 node를 연결하는 선을 edge라고 한다. Tree의 계층을 표현하는 level이라는 개념이 있다. Tree의 시작이 되는 최상위 node를 root node라고 하며, 이는 level 0이다.

자식 node가 없는 최하위 node를 leaf node 또는 terminal(단말) node라고 한다. 단말 node가 아닌 degree가 1 이상인 node는 internal(내부) node라고 한다.

Subtree는 특정 node를 root로 하는 작은 tree를 의미한다. 위 그림에서 `2`는 `7`, `5`를 root로 하는 두 개의 subtree를 가지고 있다. **한 node가 가진 subtree의 수를 그 node의 degree(차수)**라고 한다. Tree의 node 중 가장 높은 degree를 가지는 node의 degree가 그 tree의 degree가 된다.

Tree의 **depth(깊이)는 root에서 자신에게 도달하기 위해 거치는 edge의 수**이다. 위 그림에서 `10`의 depth는 2이다. Root node의 depth는 0이다. Tree의 **height는 root에서 가장 멀리 떨어진(깊은) node까지의 depth**이다. 위 그림에서 tree의 height는 3이다.

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

5. traversal(순회)

   Traversal은 tree의 모든 node를 빠뜨리지 않고 방문하는 과정이다. 순회할 때 하나의 node에서 선택할 수 있는 행동은 다음 세 가지이다.

   1. D: 현재 node를 방문한다.

   2. L: 왼쪽 subtree를 방문한다.

   3. R: 오른쪽 subtree를 방문한다.

   이 세 가지 작업을 어떤 순서로 수행하느냐에 따라 다음과 같이 세 가지 순회 방법이 있다:

   1. Preorder traversal(전위 순회)

      **D, L, R** 순서로 방문한다.

   2. Inorder traversal(중위 순회)

      **L, D, R** 순서로 방문한다.

   3. Postorder traversal(후위 순회)

      **L, R, D** 순서로 방문한다.

   각각의 순회 방법은 재귀 함수를 이용하여 구현할 수 있다.

---

## Binary Search Tree

1. 이해

   Binary search tree는 기존 binary tree에서 원소 탐색의 효율성을 높이기 위해 원소의 크기에 따라 node 위치를 정의한 tree이다. Binary search tree의 조건은 다음과 같다.

   1. **모든 node는 서로 다른 유일한 키**를 가진다.

   2. 왼쪽 subtree에 있는 모든 node의 key 값은 부모 node의 key 값보다 작다.

      왼쪽 node의 key 값은 부모 node의 key 값보다 작다.

   3. 오른쪽 subtree에 있는 모든 node의 key 값은 부모 node의 key 값보다 크다.

      오른쪽 node의 key 값은 부모 node의 key 값보다 크다.

   4. **왼쪽, 오른쪽 subtree도 각각 binary search tree**이다.

2. 탐색

   우선 찾고자 하는 값 `n`을 root node의 key값 역할을 하는 `data`와 비교하여, 만약 작으면 왼쪽 subtree에서 탐색하고, 크면 오른쪽 subtree에서 탐색한다. 이 과정을 재귀적으로 반복하여 원하는 key 값을 가진 node를 찾을 수 있다.

   ```C
   TreeNode* search(TreeNode* root, char data) {
      TreeNode* p = root;
      while (p != NULL) {
         if (data < p->data) {
               p = p->left;
         } else if (data == p->data) {
               return p;
         } else if (data > p->data) {
               p = p->right;
         }
      }
   }
   ```

3. 삽입

   Binary search tree에 새로운 원소를 삽입하기 전에 같은 원소가 있는지를 확인하는 과정이 필요하다. 탐색을 수행하여 탐색이 실패한 위치에 새로운 node를 삽입한다. 모든 node의 key 값은 서로 달라야 하므로, 만약 같은 원소가 이미 있으면 삽입하지 않는다.

   ```c
   TreeNode* insert(TreeNode* p, char data) {
      if (p == NULL) {
         TreeNode* newNode = (TreeNode*)malloc(sizeof(TreeNode));
         newNode -> data = data;
         newNode -> left = NULL;
         newNode -> right = NULL;
         return newNode;
      }
      if (data < p -> data) {
         p -> left = insert(p -> left, data);
      } else if (data > p -> data) {
         p -> right = insert(p -> right, data);
      } else {
         printf("이미 같은 값을 가진 node가 있어요");
      }
      return p;
   }
   ```

4. 삭제

   Binary search tree에서 원소를 삭제하는 경우에는 삭제하고자 하는 node의 자식 node의 수에 따라 다음과 같이 세 가지 경우로 나누어 처리한다.

   1. 삭제하고자 하는 node가 leaf node인 경우

      그냥 삭제하고, 부모 node의 자식 링크를 NULL로 설정한다.

   2. 삭제하고자 하는 node가 하나의 자식 node를 가지는 경우

      삭제하고자 하는 node를 삭제하고, 자식 node를 부모 node와 직접 연결한다.

   3. 삭제하고자 하는 node가 두 개의 자식 node를 가지는 경우

      삭제하고자 하는 node의 왼쪽 subtree에서 가장 큰 값을 가진 node, 또는 오른쪽 subtree에서 가장 작은 값을 가진 node를 찾아 후계자로 설정하고 삭제하고자 하는 node와 교체한다.

   ```c
   TreeNode* delete(TreeNode* root, char data) {
      TreeNode *parent = NULL;
      TreeNode *p = root;

      while ((p != NULL) && (p -> data != data)) {
         parent = p;
         if (data < p -> data) {
               p = p->left;
         } else if (data > p -> data) {
               p = p->right;
         }
      }

      if (p == NULL) {
         return;
      }

      if ((p->left == NULL) && (p->right == NULL)) {
         if (parent != NULL) {
               if (parent -> left == p) {
                  parent -> left = NULL;
               } else if (parent -> right == p) {
                  parent -> right = NULL;
               }
         } else {
               root = NULL;
         }
      } else if((p->left == NULL) || (p->right == NULL)) {
         TreeNode* child;
         if (p->left == NULL) {
               child = p->left;
         } else if (p->right == NULL) {
               child = p->left;
         }
         if (parent != NULL) {
               if (parent -> left == p) {
                  parent -> left = child;
               } else if (parent -> right == p) {
                  parent -> right = child;
               }
         } else {
               root = child;
         }
      } else {
         TreeNode *successorParent = p;
         TreeNode *successor = p->left;
         while (successor->right != NULL) {
               successorParent = successor;
               successor = successor->right;
         }
         if (successorParent->left != successor) {
               successorParent->left = successor->left;
         } else if (successorParent->right == successor) {
               successorParent->right = successor->left;
         }
         p->data = successor->data;
         p = successor;
      }
      free(p);
   }
   ```

---

## AVL Tree

1. 이해

   > AVL Tree는 대표적인 balanced binary search tree이다.

   AVL Tree는 모든 node의 왼쪽, 오른쪽 subtree의 height 차이가 1 이하인 binary search tree이다. left subtree의 height를 $h_L$, right subtree의 height를 $h_R$이라고 할 때, balance factor는 $h_L-h_R$이다. 이에 관하여 AVL Tree의 특징은 다음과 같다.

   1. left subtree < parent node < right subtree의 관계를 만족한다.

   2. 모든 node의 balance factor는 -1, 0, 1 중 하나이다.

      만약 그렇지 않다면 rotation을 통해 균형을 맞춘다.

2. 회전

   AVL Tree에서의 불균형과 그에 따른 회전 연산은 다음 네 가지 경우로 나뉜다.

   1. LL

      불균형 발생 node의 left child와 그의 left child가 존재하는 경우이다.

      ![image](https://github.com/user-attachments/assets/5694d38e-7281-4eeb-a759-16150c79572a)

   2. LR

      불균형 발생 node의 left child와 그의 right child가 존재하는 경우이다.

      ![image](https://github.com/user-attachments/assets/7d8767b9-e847-4641-89f6-7db356d6d2d7)

   3. RL

      불균형 발생 node의 right child와 그의 left child가 존재하는 경우이다.

      ![image](https://github.com/user-attachments/assets/7327b1c9-eeb4-434f-8f4f-09a20653068f)

   4. RR

      불균형 발생 node의 right child와 그의 right child가 존재하는 경우이다.

      ![image](https://github.com/user-attachments/assets/e001c7bb-722a-4230-ac56-5dcae51928a4)

---
