
## 동기와 비동기

<img width="500" alt="Image" src="https://github.com/user-attachments/assets/1b4a4e98-70be-42eb-9d79-bd34abb6973a" />

처리 시간이 10초인 함수 task1과 7초인 함수 task2가 순서대로 호출되었다고 가정할 때, 

1. task1이 종료될 때 까지 task2가 기다리는 방식이 **동기(synchronous)**처리
2. task1이 종료되지 않았음에도 task2를 실행하는 방식이 **비동기(asynchronous)**처리

이렇게 동기와 비동기가 나뉜다.

이 예시에서 동기의 경우는 task2가 task1이 처리되는 10초동안 실행되지 못하고 blocking된다는 단점이 있다. 그러나 순서대로 하나씩 처리하므로 실행 순서가 보장되어 오류 처리가 쉽다.

비동기는 task2가 task1을 기다리지 않기 때문에 blocking이 발생하지 않지만(non-blocking), 각 task의 실행 순서가 불명확하다는 단점이 있다.
