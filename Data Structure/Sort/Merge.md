## 이게 머지

1. 이해

   Merge sort는 divide and conquer(분할 정복) 기법을 채용한 sort algorithm이다.

   1. 주어진 array를 2등분하여 부분 array를 만든다.

      이 과정을 recursive call을 통해 반복한다.

   2. 나눠진 부분 array들을 정렬하면서 병합한다.

   $n$개의 원소를 2개로 분할하기 위해 $log_2 n$번 반복하고, 각 부분을 비교하며 병합하는 과정에서 $n$번의 비교를 수행하기 때문에 시간복잡도는 $O(n log_2 n)$이다.

2. 구현

   다음 코드는 주어진 array를 정렬하면서 병합하는 과정을 구현한 것이다.

   ```c
    void merge(int array[], int begin, int middle, int end) {
        int left = begin;
        int right = middle + 1;
        int sortedIndex = begin;

        while (left <= middle && right <= end) {
            if (array[left] <= array[right]) {
                sorted[sortedIndex++] = array[left++];
            } else {
                sorted[sortedIndex++] = array[right++];
            }
        }

        while (left <= middle) {
            sorted[sortedIndex++] = array[left++];
        }

        while (right <= end) {
            sorted[sortedIndex++] = array[right++];
        }

        for (int i = begin; i <= end; i++) {
            array[i] = sorted[i];
        }
    }
   ```

   이 코드에서는 while문을 통해 두 부분 array에서 첫 번째 원소부터 하나씩 비교하여 정렬된 원소를 `sorted` array에 저장한다. 이렇게 한쪽의 모든 원소를 `sorted`에 넣고 나서 다른 한쪽에 남아있는 원소들을 그대로 `sorted`에 넣는다.

   마지막으로 `sorted` array의 원소들을 원래 array에 복사한다.

   이 `merge()` 함수를 다음과 같이 재귀적으로 호출하여 merge sort를 구현할 수 있다.

   ```c
    void mergeSort(int array[], int begin, int end) {
        if (begin < end) {
            const int middle = (begin + end) / 2;
            mergeSort(array, begin, middle);
            mergeSort(array, middle + 1, end);
            merge(array, begin, middle, end);
        }
    }
   ```

   이 코드에서도 recursive call을 통해 array의 앞부분과 뒷부분에 대해 분할을 작업을 반복한다.

---
