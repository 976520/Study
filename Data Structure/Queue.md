# Q

> Queue는 data를 순서대로 처리하는 자료구조이다.

---

## 이해

![image](https://github.com/user-attachments/assets/40f1f774-cabe-4925-8a49-647a6ac5ef3b)

Queue의 맨 앞에 있는 data를 가리키는 pointer를 front, 가장 마지막에 삽입된 data를 가리키는 pointer를 rear라고 한다. 삭제 연산인 `deQueue`는 front에서만, 삽입 연산인 `enQueue`는 rear에서만 이루어진다. 따라서 **가장 먼저 삽입된 data가 가장 먼저 삭제**되며, 이를 First In First Out(FIFO)이라고 한다.

---
