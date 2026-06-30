## bellman-ford

1. 이해

   Bellman-Ford는 모든 edge에 대한 relaxation을 반복하여 최단 경로를 구하는 방법이다. Dijkstra와 달리 **음의 가중치가 있어도 사용할 수 있고, negative cycle의 존재 여부도 판별할 수 있다.**

   최단 경로는 cycle을 포함하지 않으므로 최대 $V - 1$개의 edge로 이루어진다. 따라서 모든 edge에 대한 relaxation을 $V - 1$번 반복하면 모든 vertex의 최단 경로가 확정된다.

   1. distance array를 무한대로 초기화하고 시작 vertex만 0으로 설정한다.

   2. 모든 edge $(u, v)$에 대해 $distance[u] + w(u, v) < distance[v]$이면 갱신하는 relaxation을 수행한다.

   3. 2번 과정을 $V - 1$번 반복한다.

   4. $V - 1$번 반복한 뒤에도 갱신되는 edge가 존재하면, negative cycle이 존재하는 것이다.

   $V - 1$번 반복한 후에는 더 이상 갱신이 일어나지 않아야 하는데, 한 번 더 수행했을 때 여전히 갱신되는 edge가 있다면 그것은 돌수록 distance가 줄어드는 negative cycle이 있다는 의미이다.

2. 구현

   ```c
   typedef struct Edge {
     int start;
     int end;
     int weight;
   } Edge;

   int bellmanFord(Edge edges[], int edgeCount, int distance[], int n, int start) {
     int i, j;

     for (i = 0; i < n; i++) {
       distance[i] = INF;
     }
     distance[start] = 0;

     for (i = 0; i < n - 1; i++) {
       for (j = 0; j < edgeCount; j++) {
         int u = edges[j].start;
         int v = edges[j].end;
         int w = edges[j].weight;
         if (distance[u] != INF && distance[u] + w < distance[v]) {
           distance[v] = distance[u] + w;
         }
       }
     }

     for (j = 0; j < edgeCount; j++) {
       int u = edges[j].start;
       int v = edges[j].end;
       int w = edges[j].weight;
       if (distance[u] != INF && distance[u] + w < distance[v]) {
         return 1; // negative cycle 존재
       }
     }
     return 0;
   }
   ```

   모든 edge에 대한 relaxation을 $V - 1$번 반복한 뒤, 한 번 더 수행하여 갱신이 일어나면 negative cycle이 있다고 판단하여 1을 반환한다.

---
