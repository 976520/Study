# 쉘 정렬

1. 이해

   Shell sort는 일정한 interval(간격)을 두고 떨어진 요소들끼리 부분집합을 만들어 insertion sort를 수행하는 것이다. insertion sort은 거의 정렬된 요소들에 대해서는 매우 빠른 속도를 보이기 때문에 이를 응용하여 효율을 높이는 것이다.

   1. interval을 정하고, interval 만큼 떨어진 요소들끼리 부분집합을 만든다.

   2. 부분집합에 대해 insertion sort를 수행한다.

   3. interval을 1이 될 때까지 $1/2$씩 줄여가며 반복한다.

   일반적으로 shell sort의 시간복잡도는 interval에 따라 달라지기는 하지만, $O(n^{1.25})$라고 한다.

2. 구현

   Shell sort의 기반이 insertion sort이기 때문에, 이를 먼저 구현해야 한다.

   ```c
   void insertionSort(int array[], int begin, int end, int interval) {

   }
   ```

---
