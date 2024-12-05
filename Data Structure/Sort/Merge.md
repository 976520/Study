## 이게 머지

1. 이해

   Merge sort는 divide and conquer(분할 정복) 기법을 채용한 sort algorithm이다.

   1. 주어진 array를 2등분하여 부분 array를 만든다.

      이 과정을 recursive call을 통해 반복한다.

   2. 나눠진 부분 array들을 정렬하면서 병합한다.

   $n$개의 원소를 2개로 분할하기 위해 $log_2 n$번 반복하고, 각 부분을 비교하며 병합하는 과정에서 $n$번의 비교를 수행하기 때문에 시간복잡도는 $O(n log_2 n)$이다.

2. 구현

   ```c

   ```

---
