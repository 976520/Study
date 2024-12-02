## 퀵 정렬

1. 이해

   Quick sort는 분할 정복을 이용한 정렬 알고리즘 중 하나로, 원소 하나를 pivot으로 설정하고 그를 기준으로 작은 것들과 큰 것들로 나눈다. 나누어진 array에서 다시 pivot을 설정하고 나누는 과정을 재귀적으로 반복한다.

2. 구현

   실질적인 정렬을 하기 전에 `pivot`의 위치를 정하여 `array`를 분할하는 과정이 필요하다. 이를 함수로 나타내면 다음과 같다. 여기서는 `pivot`을 중간 원소로 설정하였다.

   ```c
    int partition(int array[], int begin, int end, int length) {
        int L = begin;
        int R = end;
        int pivot = (begin + end) / 2;
        int temp;

        while (L < R) {
            while ((array[L] < array[pivot]) && (L < R)) {
                L++;
            }
            while ((array[R] > array[pivot]) && (R > L)) {
                R--;
            }
            if (L < R) {
                temp = array[L];
                array[L] = array[R];
                array[R] = temp;
                if (L == pivot) {
                    pivot = R;
                }
            }
        }
        temp = array[pivot];
        array[pivot] = array[R];
        array[R] = temp;
        return R;
    }
   ```

   위 코드에서 `L`은 왼쪽에서 오른쪽으로, `R`은 오른쪽에서 왼쪽으로 이동하며 `pivot`을 기준으로 정렬되지 않은 원소를 찾는다. 이 `L`과 `R`이 각각 `pivot`보다 크거나 같은 원소와 `pivot`보다 작거나 같은 원소를 찾으면, 두 원소의 위치를 교환한다. `pivot`의 왼쪽에는 `pivot`보다 작은 원소들이, 오른쪽에는 `pivot`보다 큰 원소들이 오게 해야 하기 때문이다. 이때 교환하는 원소 중 하나가 `pivot`이면 `pivot`의 위치도 함께 갱신한다.

   이 과정을 `L`과 `R`이 만날 때까지 반복한다. `L`과 `R`이 만나면 `pivot`과 `R`이 가리키는 원소의 위치를 교환하고 `R`을 반환한다. 이렇게 반환된 `R`은 다음 정렬에서의 `pivot`이 된다.

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
