## dijkstra

1. 이해

   Dijkstra는 시작 vertex에서 가장 가까운 vertex부터 차례로 최단 경로를 확정해 나가는 greedy(탐욕) 방법이다.

   아직 확정되지 않은 vertex 중에서 시작점으로부터의 distance가 가장 작은 vertex를 선택하여 확정하고, 그 vertex를 거쳐 인접 vertex로 가는 distance가 기존보다 짧아지면 갱신한다. 이렇게 distance를 짧게 갱신하는 과정을 relaxation(완화)이라고 한다.

   1. distance를 저장할 array를 정의하고 모든 값을 무한대로 초기화한다.

      시작 vertex의 distance만 0으로 설정한다.

   2. 확정되지 않은 vertex 중에서 distance가 가장 작은 vertex $u$를 선택하여 확정한다.

   3. $u$에 인접한 vertex $v$에 대해 $distance[u] + w(u, v) < distance[v]$이면 $distance[v]$를 갱신한다.

   4. 모든 vertex가 확정될 때까지 2번과 3번을 반복한다.

   매번 distance가 가장 작은 vertex를 빠르게 찾기 위해 **priority queue(우선순위 큐)** 를 사용하면 시간 복잡도가 $O((V + E)\log V)$가 된다.

   가장 가까운 vertex를 확정할 때, 그 vertex로 가는 더 짧은 경로가 이후에 발견되지 않는다는 것이 전제이다. 따라서 edge weight가 음수이면 이 전제가 깨지므로 dijkstra는 **음의 가중치가 있는 graph에서는 사용할 수 없다.**

2. 구현

   ```c
   void dijkstra(int graph[][MAX_VERTEX], int distance[], int n, int start) {
     int visited[MAX_VERTEX] = {0};
     int i, u, v;

     for (i = 0; i < n; i++) {
       distance[i] = INF;
     }
     distance[start] = 0;

     for (i = 0; i < n; i++) {
       u = -1;
       for (v = 0; v < n; v++) {
         if (!visited[v] && (u == -1 || distance[v] < distance[u])) {
           u = v;
         }
       }
       if (distance[u] == INF) {
         break;
       }
       visited[u] = 1;

       for (v = 0; v < n; v++) {
         if (!visited[v] && graph[u][v] != INF &&
             distance[u] + graph[u][v] < distance[v]) {
           distance[v] = distance[u] + graph[u][v];
         }
       }
     }
   }
   ```

   위 코드에서 확정되지 않은(`visited[v] == 0`) vertex 중 `distance`가 가장 작은 `u`를 선택하여 확정하고, `u`에 인접한 vertex에 대해 relaxation을 수행한다. Priority queue를 사용하면 가장 작은 `u`를 찾는 과정을 $O(\log V)$로 줄일 수 있다.

---
