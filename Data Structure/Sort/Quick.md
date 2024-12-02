## 퀵 정렬

1. 이해

   Quick sort는 분할 정복을 이용한 정렬 알고리즘 중 하나이다.

   1. pivot을 선택한다.

      보통 중간 원소를 선택한다.

   2. pivot을 기준으로 array를 분할한다.

      pivot보다 작은 원소들은 왼쪽으로, 큰 원소들은 오른쪽으로 이동시킨다.

   3. 분할된 각각의 부분 array의 크기가 1이 될 때까지 각각에 대해 이 과정을 재귀적으로 반복한다.

   평균적으로 시간 복잡도가 $O(n\log n)$이지만, pivot이 최소값이나 최대값인 최악의 경우 $O(n^2)$이다.

2. 구현

   실질적인 정렬을 하기 전에 `pivot`의 위치를 정하여 `array`를 분할하는 과정이 필요하다. 이를 함수로 나타내면 다음과 같다. 여기서는 `pivot`을 중간 원소로 설정하였다.

   ```c
    int partition(int array[], int begin, int end, int length) {
        int left = begin;
        int right = end;
        int pivot = (begin + end) / 2;
        int temp;

        while (left < right) {
            while ((array[left] < array[pivot]) && (left < right)) {
                left++;
            }
            while ((array[right] > array[pivot]) && (right > left)) {
                right--;
            }
            if (left < right) {
                temp = array[left];
                array[left] = array[right];
                array[right] = temp;
                if (left == pivot) {
                    pivot = right;
                }
            }
        }
        temp = array[pivot];
        array[pivot] = array[right];
        array[right] = temp;
        return right;
    }
   ```

   위 코드에서 `left`은 왼쪽에서 오른쪽으로, `right`은 오른쪽에서 왼쪽으로 이동하며 `pivot`을 기준으로 정렬되지 않은 원소를 찾는다. 이 `left`과 `right`이 각각 `pivot`보다 크거나 같은 원소와 `pivot`보다 작거나 같은 원소를 찾으면, 두 원소의 위치를 교환한다. `pivot`의 왼쪽에는 `pivot`보다 작은 원소들이, 오른쪽에는 `pivot`보다 큰 원소들이 오게 해야 하기 때문이다. 이때 교환하는 원소 중 하나가 `pivot`이면 `pivot`의 위치도 함께 갱신한다.

   이 과정을 `left`과 `right`이 만날 때까지 반복한다. `left`과 `right`이 만나면 `pivot`과 `right`이 가리키는 원소의 위치를 교환하고 `right`을 반환한다. 이렇게 반환된 `right`은 다음 정렬에서의 `pivot`이 된다.

   여기서 계속 재귀 호출을 해가며 정렬을 할 수 있다.

   ```c
    void quickSort(int array[], int begin, int end, int length) {
        if (begin < end) {
            const int pivot = partition(array, begin, end, length);
            quickSort(array, begin, pivot - 1, length);
            quickSort(array, pivot + 1, end, length);
        }
    }
   ```

---
