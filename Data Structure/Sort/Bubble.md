## 버블 정렬

1. 이해

   <img src="https://github.com/user-attachments/assets/0ec63b6c-4278-4432-8c09-367725a19185" alt="bubble" width="500" />

   Bubble sort의 과정은 다음과 같다.

   1. 인접한 두 수를 선택한다

   2. 두 수가 정렬되어 있지 않는 경우에만 두 수의 위치를 바꾼다.

   3. 배열에 변화가 없을 때까지 반복한다.

   모든 경우에서 시간 복잡도가 $O(n^2)$으로, 매우 비효율적인 알고리즘으로 꼽힌다.

2. 구현

   중첩 for문을 이용하여 구현할 수 있다.

   1번째와 2번째 요소를 비교하고, 2번째와 3번째 요소를 비교하고... $n - 1$번째와 $n$번째 요소를 비교한 뒤, 다시 처음으로 돌아가 1번째와 2번째 요소를 비교하고 이번에는 $n - 2$번째와 $n - 1$번째 요소를 비교하고 이짓을 반복한다. 따라서 최악의 경우 맨 안쪽의 인접한 두 수를 비교하는 if문이 $\frac{n(n - 1)}{2}$번 실행된다.

   ```c
   void bubbleSort(int array[], int length) {
     for (int i = 0; i < length - 1; i++) {
       for (int j = 0; j < length - 1 - i; j++) {
          if (array[j] > array[j + 1]) {
              const int temp = array[j];
              array[j] = array[j + 1];
              array[j + 1] = temp;
          }
        }
      }
    }
   ```

   이때 array의 마지막 요소부터 정렬되는 것을 확인할 수 있다.

---
