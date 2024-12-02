## 선택 정렬

1. 이해

   Selection sort의 과정은 다음과 같다.

   1. 처음부터 끝까지 순회하며 최소값을 찾는다.

   2. 앞으로 보낸다.

      이렇게 앞으로 보내진 원소는 정렬된 것으로 간주한다.

   3. 이미 정렬된 부분을 제외하고 같은 연산을 모든 부분이 정렬될 때까지 반복한다.

   모든 경우에서 시간 복잡도가 $O(n^2)$으로, 비효율적인 알고리즘으로 꼽힌다.

2. 구현

   ```c
   void selectionSort(int array[], int length) {
      for (int i = 0; i < length - 1; i++) {
         int min = i;
         for(int j = i + 1; j < length; j++) {
               if (array[j] < array[min]) {
                  min = j;
               }
         }
         const int temp = array[i];
         array[i] = array[min];
         array[min] = temp;
      }
   }
   ```

---
