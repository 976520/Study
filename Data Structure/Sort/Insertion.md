## 삽입 정렬

1. 이해

   ![Insertion](https://github.com/user-attachments/assets/f6887c01-1024-4193-8772-ba8f162a76e3)

   Insertion sort에서는 정렬할 array가 Sorted와 Unsorted의 두 부분집합으로 나뉘어 있다고 가정한다. 정렬 된 앞부분의 원소는 Sorted, 정렬되지 않은 뒷부분의 원소는 Unsorted이다.

   1. Unsorted 집합에서 원소를 선택하여 key로 설정한다.

      첫 번째 원소는 Sorted라고 가정하고, 두 번째 원소부터 시작한다.

   2. key를 Sorted 집합의 모든 원소와 비교하여 삽입할 위치를 찾는다.

      이때 Sorted의 마지막 원소부터 비교한다.

   3. 찾은 위치에 삽입한다.

      삽입한 위치 이후의 원소들을 한 칸씩 뒤로 이동한다.

   4. key를 다음 위치로 이동한다.

   5. key가 Unsorted 집합의 마지막 원소가 될 때까지 반복한다.

2. 구현

   ```c
   void insertionSort(int array[], int length) {
       for (int i = 1; i < length; i++) {
           const int key = array[i];
           int j = i;
           while ((j > 0) && (array[j - 1] > key)) {
               array[j] = array[j - 1];
               j--;
           }
           array[j] = key;
       }
   }
   ```

   위 코드에서 `key` 변수는 Unsorted 집합에서 정렬하기 위해 선택한 원소이다.

   `i`는 Sorted 집합과 Unsorted 집합의 경계를 나타낸다. `i` 미만의 index를 가진 원소들은 Sorted 집합에 속하고, `i` 이상의 index를 가진 원소들은 Unsorted 집합에 속한다.

   `j`는 `key`가 삽입될 위치를 찾기 위해 Sorted 집합을 탐색할 때 사용된다. `j`는 `i`에서 시작하여 `key`보다 큰 원소를 만날 때마다 감소하면서 삽입 위치를 찾아간다.

   while문은 `key`가 삽입될 위치를 찾기 위해 Sorted 집합을 탐색하는 과정이다. `j`가 0보다 크고, `array[j - 1]`이 `key`보다 크면, `array[j]`와 `array[j - 1]`의 값을 교환하고 `j`를 감소시킨다.

---
