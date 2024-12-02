## 삽입 정렬

1. 이해

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

   첫 번째 for문에서 정렬 대상 원소의 index `i`를 `j`에 할당한다.

---
