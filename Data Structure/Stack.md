# https://stackoverflow.com/

> Stack은 data를 쌓아 올린 형태의 자료구조이다.

---

## 이해

Stack의 맨 위 data를 가리키는 pointer를 top이라고 하고, data를 삽입하는 연산을 ~~git~~ push, 삭제하는 연산을 pop이라고 한다. 이 top에서만 data를 push하거나 pop할 수 있다. 따라서 data가 여러 번 push되는 경우 **top을 통해 가장 먼저 삽입된 data가 가장 나중에 삭제**되며, 이를 Last In First Out(LIFO)이라고 한다.

---

## 구현

Stack은 두 가지 방법으로 구현할 수 있다.

1.  array

    1차원 array를 이용하여 stack을 구현할 수 있다. `stack[MAX_STACK_SIZE]`을 만들어서 첫 번째 원소를 `stack[0]`에 넣고, 두 번째 원소를 `stack[1]`에 넣고 하는 식이다. 이 경우 **stack의 최대 크기를 미리 정해야 하며**, 이를 변경할 수 없다.

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

2.  linked list

    Array를 이용한 stack의 구현에서는 최대 크기를 미리 정해야 하는 단점이 있었다. Linked list를 이용하면 이를 극복할 수 있다.

    Stack의 각 원소를 linked list의 node로 표현하면 된다. 이때 각 node는 데이터를 저장하는 data field와 다음 node를 가리키는 link field로 구성된다.

    ```c
    typedef struct StackNode {
      int data;
      struct StackNode *link;
    } StackNode;
    ```

    Stack의 top은 linked list의 head를 가리키는 pointer로 표현할 수 있다. 초기값은 아무것도 가리키지 않는 상태인 `NULL`로 설정한다.

    ```c
    StackNode *top = NULL;
    ```

    따라서 `top`이 `NULL`인 경우 stack이 비어있는 것이다.

    ```c
    int isEmpty() {
      if (top == NULL) {
        return 1;
      } else {
        return 0;
      }
    }
    ```

    Push 연산은 새로운 node를 만들어서 그 값을 `top`이 가리키게 하는 것이다.

    ```c
    void push(int item) {
      StackNode *newNode = (StackNode *)malloc(sizeof(StackNode));

      newNode->data = item;
      newNode->link = top;
      top = newNode;
    }
    ```

    Pop 연산은 `top`이 가리키는 node를 삭제하는 것이다.

    ```c
    int pop() {
      int item;
      StackNode *deleteNode = top;

      if (isEmpty()) {
        printf("stack is empty");
        return 0;
      } else {
        item = deleteNode->data;
        top = deleteNode->link;
        free(deleteNode);
        return item;
      }
    }
    ```

## 사용

Stack 자료구조는 여러 곳에서 사용된다. ~~시험문제~~

1. 문자열 역순 변환

   LIFO의 특성을 이용하여 문자열을 역순으로 출력할 수 있다.

   문자열을 순서대로 push하고, 그 순서대로 pop하면 역순으로 출력된다.

2. 수식의 후위 표기법 변환

   수식은 사실 다음 3가지 표기법으로 표현할 수 있다.

   1. 전위 표기법(prefix notation): 연산자가 피연산자의 앞에 위치하는 표기법

   2. 중위 표기법(infix notation): 연산자가 피연산자의 중간에 위치하는 표기법

      우리가 일상에서 주로 사용하는 표기법이다.

   3. 후위 표기법(postfix notation): 연산자가 피연산자의 뒤에 위치하는 표기법

      컴퓨터가 수식을 처리하기 위해 사용하는 표기법이다. 괄호나 연산자 우선순위를 따로 고려하지 않고, 표기된 순서대로 처리할 수 있기 때문이다.

   Stack을 이용하여 중위 표기법을 후위 표기법으로 변환하는 방법은 다음과 같다.

   1. 왼쪽 괄호를 만나면 무시한다.

   2. 피연산자를 만나면 바로 출력한다.

   3. 연산자를 만나면 stack에 push한다.

   4. 오른쪽 괄호를 만나면 stack에서 pop하여 출력한다.

   5. 수식이 끝나면 stack에 남아있는 모든 연산자를 pop하여 출력한다.

   또 stack을 이용하여 후위 표기법으로 표기된 수식을 계산할 수 있다.

   1. 피연산자를 만나면 stack에 push한다.

   2. 연산자를 만나면 stack에서 필요한 만큼의 피연산자를 pop하여 연산하고, 그 결과를 stack에 push한다.

   3. 수식이 끝나고 stack에 남아있는 값이 계산 결과이다.

   이를 구현한 코드는 다음과 같다.

   ```c
    int calculate(char *수식) {
      int 값;
      const int 길이 = strlen(수식);

      for (int i = 0; i < 길이; i++) {
          char 문자 = 수식[i];

          if (문자 != '+' && 문자 != '-' && 문자 != '*' && 문자 != '/') {
              값 = 문자 - '0';
              push(값);
          } else {
              int 피연산자2 = pop();
              int 피연산자1 = pop();

              switch (문자) {
                  case '+':
                      값 = 피연산자1 + 피연산자2;
                  break;
                  case '-':
                      값 = 피연산자1 - 피연산자2;
                  break;
                  case '*':
                      값 = 피연산자1 * 피연산자2;
                  break;
                  case '/':
                      값 = 피연산자1 / 피연산자2;
                  break;
              }
              push(값);
          }
      }
      return pop();
    }
   ```

   입력된 문자를 if문에서 검사하여 만약 피연산자라면 숫자로 변환하여 push한다. 문자가 연산자라면 `피연산자1`과 `피연산자2`에 각각 `pop()`한 값을 넣고, 연산자에 따라 계산한 후 그 결과를 push한다. 이 과정을 for문을 통해 수식의 길이만큼 반복하고, 마지막에 stack에 남아있는 값을 `pop()`하여 반환한다.

3. 수식의 괄호 검사

---
