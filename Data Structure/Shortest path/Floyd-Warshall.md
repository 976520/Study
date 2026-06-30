## floyd-warshall

1. 이해

   Floyd-Warshall은 모든 vertex 쌍 사이의 최단 경로를 한 번에 구하는 방법이다. Dynamic programming(동적 계획법)을 사용하여 구현한다.

   1. 0부터 $k$까지의 vertex만을 경유지로 이용하여 구한, vertex $i$에서 vertex $j$로 가는 최단 경로를 $A^k[i][j]$라고 정의한다.

   2. $A^{k-1}$까지 구한 상태에서 $A^k[i][j]$를 구할 때, $k$번째 vertex를 경유하지 않는 경우 $A^{k-1}[i][j]$와 경유하는 경우 $A^{k-1}[i][k] + A^{k-1}[k][j]$ 중 작은 값을 선택하여 저장한다.

   $$A^k[i][j] = \min(A^{k-1}[i][j],\ A^{k-1}[i][k] + A^{k-1}[k][j])$$

   3. vertex가 $n$개일 때, $A^{-1}$부터 $A^{n-1}$까지 구한다.

      $A^{-1}$은 초기값으로써 adjacency matrix 상태와 같고, $A^{n-1}[i][j]$는 모든 vertex를 경유지로 고려한 $i$에서 $j$까지의 최단 경로이다.

   세 vertex에 대한 삼중 반복문으로 구현되어 시간 복잡도가 $O(V^3)$이지만, 코드가 간결하고 음의 가중치가 있어도 사용할 수 있다. 단, $A^k[k][k]$가 음수가 되면 negative cycle이 존재하는 것이다.

2. 구현

   ```c
   void floydWarshall(int graph[][MAX_VERTEX], int distance[][MAX_VERTEX], int n) {
     int i, j, k;

     for (i = 0; i < n; i++) {
       for (j = 0; j < n; j++) {
         distance[i][j] = graph[i][j];
       }
     }

     for (k = 0; k < n; k++) {
       for (i = 0; i < n; i++) {
         for (j = 0; j < n; j++) {
           if (distance[i][k] != INF && distance[k][j] != INF &&
               distance[i][k] + distance[k][j] < distance[i][j]) {
             distance[i][j] = distance[i][k] + distance[k][j];
           }
         }
       }
     }
   }
   ```

   가장 바깥 반복문의 `k`가 경유지로 허용되는 vertex이고, 그 안에서 모든 vertex 쌍 `(i, j)`에 대해 `k`를 경유하는 경로가 더 짧은지 비교하여 갱신한다.

---
