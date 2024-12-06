## 기수 정렬

1. 이해

   ![image](https://github.com/user-attachments/assets/f5fd2218-f7e6-4e1b-a6cc-47c2c1e33a35)

   Radix sort은 정렬할 원소에 해당하는 key값을 가지는 bucket에 원소를 분배했다가, bucket의 순서대로 원소를 가져와 병합하는 방식으로 작동한다. 예를 들어 100의 자릿수 10진수 정수를 정렬한다면, 0~9까지의 10개의 bucket을 사용하여 1의자리, 10의자리, 100의자리에 따라 총 3번의 radix sort를 진행한다.

   1. 각 원소의 기수에 따라 bucket에 분배한다.

      이때 bucket은 queue로 구현한다.

   2. 이 과정을 자릿수만큼 반복한다.

---
