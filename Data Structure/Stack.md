# https://stackoverflow.com/

> Stack은 data를 쌓아 올린 형태의 자료구조이다.

---

## 이해

Stack의 맨 위 data를 가리키는 pointer를 top이라고 하고, data를 삽입하는 연산을 ~~git~~ push, 삭제하는 연산을 pop이라고 한다. 이 top에서만 data를 push하거나 pop할 수 있다. 따라서 data가 여러 번 push되는 경우 **top을 통해 가장 먼저 삽입된 data가 가장 나중에 삭제**되며, 이를 Last In First Out(LIFO)이라고 한다.

1. 구현

   Stack은 두 가지 방법으로 구현할 수 있다.

   1. array

      1차원 array를 이용하여 stack을 구현할 수 있다. `stack[MAX_STACK_SIZE]`을 만들어서 첫 번째 원소를 `stack[0]`에 넣고, 두 번째 원소를 `stack[1]`에 넣고 하는 식이다. 이 경우 stack의 최대 크기를 미리 정해야 한다.

      ```c
      int stack[MAX_STACK_SIZE];
      ```

      이때 마지막 원소의 index를 변수 `top`에 넣으면 된다. 따라서 `top`은 0부터 n-1까지의 index를 저장하게 되므로, `top`의 초기값은 -1로 설정한다.

      `top`이 -1인 경우 stack이 비어있는 것이고,

      ```c
      int isEmpty() {
        if (top == -1)
          return 1;
        else
          return 0;
      }
      ```

      `top`이 MAX_STACK_SIZE-1인 경우 stack이 가득 차있는 것이다.

      ```c
      int isFull() {
        if (top == MAX_STACK_SIZE - 1)
          return 1;
        else
          return 0;
      }
      ```

      Push 연산은 `top`을 1 증가시키고, 그 위치에 원소를 넣는 것이다. 따라서 이미 가득 차있는 경우에는 오류를 반환한다.

      ```c
      void push(int item) {
        if (isFull()) {
          printf("stack is full");
          return;
        } else {
          stack[++top] = item;
        }
      }
      ```

      Pop 연산은 `top`을 1 감소시키고, 그 위치의 원소를 반환하는 것이다. 따라서 비어있는 경우에는 오류를 반환한다.

      ```c
      int pop() {
        if (isEmpty()) {
          printf("stack is empty");
          return;
        } else {
          return stack[top--];
        }
      }
      ```

   2. linked list

---
