# Q

> Queue는 data를 순서대로 처리하는 자료구조이다.

---

## 이해

<img src="https://github.com/user-attachments/assets/40f1f774-cabe-4925-8a49-647a6ac5ef3b" alt="image" style="width: 500;">

Queue의 맨 앞에 있는 data를 가리키는 pointer를 front, 가장 마지막에 삽입된 data를 가리키는 pointer를 rear라고 한다. 삭제 연산인 `deQueue`는 front에서만, 삽입 연산인 `enQueue`는 rear에서만 이루어진다. 따라서 **가장 먼저 삽입된 data가 가장 먼저 삭제**되며, 이를 First In First Out(FIFO)이라고 한다.

---

## 구현

Queue는 두 가지 방법으로 구현할 수 있다.

1. array

   1차원 array를 이용하여 queue를 구현할 수 있고, 이를 순차(sequential) queue라고 한다. `queue[MAX_QUEUE_SIZE]`를 만든다. 변수 `front`에는 array에 저장된 data 중 첫 번째 data의 index를 저장하고, `rear`에는 마지막 data의 index를 저장한다. 이때 `front`와 `rear`의 초기값은 -1로 설정한다.

   ```c
   typedef struct {
      char queue[MAX_QUEUE_SIZE];
      int front, rear;
   } QueueType;
   ```

   Queue가 공백인 조건은 다음과 같다.

   1. Queue가 초기화되어 `front`와 `rear`가 둘다 -1인 경우

   2. `front`와 `rear`가 같은 경우

      `rear`에 있던 마지막에 삽입된 원소를 `deQueue`한 경우이다.

   따라서 다음과 같이 queue의 공백 상태를 검사할 수 있다.

   ```c
   int isEmpty(QueueType *queue) {
     if (queue->front == queue->rear) {
       return 1;
     } else {
       return 0;
     }
   }
   ```

   Array로 구현한 queue의 경우 array의 크기가 포화 상태의 조건이 된다.

   ```c
   int isFull(QueueType *queue) {
     if (queue->rear == MAX_QUEUE_SIZE - 1) {
       return 1;
     } else {
       return 0;
     }
   }
   ```

   `enQueue`에서는 `rear`를 1 증가시켜 삽입할 자리를 만들고, 그 위치에 data를 삽입한다. 포화 상태인 경우 연산을 중단한다.

   ```c
   void enQueue(QueueType *queue, char item) {
     if (isFull(queue)) {
       printf("포화 상태\n");
       return;
     } else {
       queue->rear++;
       queue->queue[queue->rear] = item;
     }
   }
   ```

   `deQueue`에서는 `front`를 1 증가시켜 삭제할 자리를 만들고, 그 위치에 있는 data를 삭제한다. 공백 상태인 경우 연산을 중단한다.

   `deQueue` 연산이 끝난 후 `front`가 가리키던 data는 삭제되고 없는 상태가 된다.

   ```c
   char deQueue(QueueType *queue) {
     if (isEmpty(queue)) {
       printf("공백 상태\n");
       return 0;
     } else {
       queue->front++;
       return queue->queue[queue->front];
     }
   }
   ```

2. linked list

   순차 queue의 경우 최대 크기를 미리 정해야 하는 단점이 있었다. Linked list를 이용한 연결(linked) queue를 이용하면 이를 극복할 수 있다.

   연결 queue의 원소는 data field와 link field로 구성된 node로 표현하고,

   ```c
   typedef struct QueueNode {
      char data;
      struct QueueNode *link;
   } QueueNode;
   ```

   `front`와 `rear`는 각각 첫 번째 node와 마지막 node를 가리키는 pointer로 표현한다.

   ```c
   typedef struct {
      QueueNode *front, *rear;
   } QueueType;
   ```

   `front`와 `rear`의 초기값은 `NULL`로 설정하여 queue를 초기화한다.

   ```c
   QueueType *createQueue() {
     QueueType *queue = (QueueType *)malloc(sizeof(QueueType));
     queue->front = NULL;
     queue->rear = NULL;
     return queue;
   }
   ```

   `front`가 NULL인 경우 연결된 node가 없는 것이므로 queue가 공백 상태이다.

   ```c
   int isEmpty(QueueType *queue) {
     if (queue->front == NULL) {
       return 1;
     } else {
       return 0;
     }
   }
   ```

   연결 queue는 크기를 정해 놓지 않고 필요할 때마다 node를 생성하여 삽입하므로 포화 상태가 존재하지 않는다.

   연결 queue에서의 `enQueue`는 새로은 node를 생성하고, 새로 삽입된 node는 마지막 node이므로, link field에 `NULL`을 저장한다. 그리고 `rear`의 link field가 새로 삽입된 node를 가리키도록 한다.

   Queue가 공백 상태인 경우 삽입할 새 node가 처음이자 마지막 node이므로, `front`와 `rear`가 모두 새로 삽입된 node를 가리키도록 한다. Queue가 공백 상태가 아닌 경우 현재 queue의 마지막 node를 가리키고 있던 `rear`의 link field가 새로 삽입된 node를 가리키도록 한다.

   ```c
   void enQueue(QueueType *queue, char item) {
      QueueNode *newNode = (QueueNode *)malloc(sizeof(QueueNode));
      newNode -> data = item;
      newNode -> link = NULL;

      if (queue->front == NULL) {
         queue->front = newNode;
         queue->rear = newNode;
      } else {
         queue->rear -> link = newNode;
         queue->rear = newNode;
      }
   }
   ```

   `deQueue`는 현재 queue의 첫 번째 node를 가리키는 `front`가 가리키는 node를 `delete`가 가리키게 하고, 그 다음 node인 `front -> link`를 `front`가 가리키도록 한다. 만약 현재 queue의 node가 1개여서 재설정한 `front`가 `NULL`을 가리키는 경우 `rear`도 `NULL`을 가리키도록 한다.

   ```c
   char deQueue(QueueType *queue) {
      QueueNode *delete = queue->front;
      char item;

      if (isEmpty(queue)) {
        printf("공백 상태\n");
        return 0;
      } else {
        item = delete->data;
        queue->front = queue->front->link;
        if (queue->front == NULL) {
          queue->rear = NULL;
        }
        free(delete);
        return item;
      }
   }
   ```

---

## 원형 queue

1. 이해

   순차 queue에서 포화 상태인지 검사할 때 `rear`가 array의 마지막 index와 같은지 검사하였다. 하지만 아래와 같은 경우 queue에 빈 자리가 많지만 `rear`가 마지막 index를 가리키고 있기 때문에 포화 상태로 인식하는 문제가 발생한다.

   <img src="https://github.com/user-attachments/assets/8662ebb3-8d5a-4bc5-a57a-9b8d3d575341" alt="image" style="width: 600;">

   이를 해결하기 위해 원형(circular) queue를 사용한다. 원형 queue는 순차 queue와 같은 방법으로 구현하되, array의 처음과 끝이 연결되어 있는 것처럼 처리하는 방법이다.

2. 구현

   원형 queue는 순차 queue처럼 1차원 array를 이용하여 구현한다.

   ```c
   typedef struct {
      char queue[MAX_QUEUE_SIZE];
      int front, rear;
   } QueueType;
   ```

   원형 queue에서는 공백 상태와 포화 상태의 구분을 위해 자리를 하나 비워둔다. 순차 queue에서는 `front`를 1 증가시키고 `rear`를 1 증가시키는 방법으로 삽입과 삭제를 수행하였다. 원형 queue에서는 index가 n-1 다음 0이 되어야 하므로 **`front`와 `rear`를 1 증가시키고 배열의 크기로 나눈 나머지를 사용한다.**

   `front`와 `rear`의 초기값을 0으로 설정하여 queue를 초기화한다.

   ```c
   QueueType *createQueue() {
      QueueType *queue = (QueueType *)malloc(sizeof(QueueType));
      queue->front = 0;
      queue->rear = 0;
      return queue;
   }
   ```

   원형 queue가 공백인 조건은 다음과 같이 초기화되는 값을 제외하고 선형 queue와 동일하다.

   1. Queue가 초기화되어 `front`와 `rear`가 둘다 0인 경우

   2. `front`와 `rear`가 같은 경우

      `rear`에 있던 마지막에 삽입된 원소를 `deQueue`한 경우이다.

   따라서 선형 queue와 동일하게 공백 상태를 검사할 수 있다.

   ```c
   int isEmpty(QueueType *queue) {
     if (queue->front == queue->rear) {
       return 1;
     } else {
       return 0;
     }
   }
   ```

   `rear`가 원형 queue를 한 바퀴 돌며 data를 삽입하여 queue를 모두 채우면, 다음 삽입 위치는 현재 `front`가 가리키는 위치가 된다. 따라서 포화 상태는 `front`와 `rear`가 같은 경우이다.

   ```c
   int isFull(QueueType *queue) {
     if ((queue->rear + 1) % MAX_QUEUE_SIZE == queue->front) {
       return 1;
     } else {
       return 0;
     }
   }
   ```

   `rear`를 1 증가시키고 배열의 크기로 나눈 나머지를 사용하여 `enQueue`를 구현한다.

   ```c
   void enQueue(QueueType *queue, char item) {
      if (isFull(queue)) {
        printf("포화 상태\n");
        return;
      } else {
        queue->rear = (queue->rear + 1) % MAX_QUEUE_SIZE;
        queue->queue[queue->rear] = item;
      }
   }
   ```

   `front`를 1 증가시키고 배열의 크기로 나눈 나머지를 사용하여 `deQueue`를 구현한다.

   ```c
   char deQueue(QueueType *queue) {
      if (isEmpty(queue)) {
        printf("공백 상태\n");
        return 0;
      } else {
        queue->front = (queue->front + 1) % MAX_QUEUE_SIZE;
        return queue->queue[queue->front];
      }
   }
   ```

---

## deque

> Double-ended queue의 약자로, 양쪽 끝에서 삽입과 삭제가 모두 가능한 queue이다.

Deque는 방향이 다른 두 개의 Queue를 붙인 형태이다.

---
