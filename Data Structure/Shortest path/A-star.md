## A\*

1. 이해

   A\*(A star)는 시작 vertex에서 특정 목적지 vertex까지의 최단 경로를 구할 때, 목적지 방향을 추정하는 heuristic(휴리스틱)을 이용하여 탐색 범위를 줄이는 방법이다.

   Dijkstra가 시작점으로부터의 실제 distance $g(n)$만으로 다음 vertex를 선택한다면, A\*는 여기에 목적지까지의 예상 distance인 heuristic $h(n)$을 더한 값 $f(n)$이 가장 작은 vertex를 우선 선택한다.

   $$f(n) = g(n) + h(n)$$

   - $g(n)$ : 시작 vertex에서 vertex $n$까지의 실제 distance
   - $h(n)$ : vertex $n$에서 목적지까지의 예상 distance
   - $f(n)$ : vertex $n$을 거치는 경로의 예상 총 distance

   1. priority queue에 시작 vertex를 $f$값과 함께 삽입한다.

   2. priority queue에서 $f$값이 가장 작은 vertex $u$를 꺼낸다.

   3. $u$가 목적지이면 종료하고, 아니면 인접 vertex에 대해 relaxation을 수행하여 $f$값과 함께 priority queue에 삽입한다.

   4. priority queue가 빌 때까지 반복한다.

   Heuristic $h(n)$이 실제 distance를 절대 과대평가하지 않으면(admissible) A\*는 항상 최단 경로를 찾는 것이 보장된다. 만약 $h(n) = 0$이면 모든 vertex에서 목적지 추정이 없는 것이므로 dijkstra와 같아진다. 격자(grid) 위에서의 경로 탐색에서는 보통 manhattan distance나 euclidean distance를 heuristic으로 사용한다.

   목적지 방향으로 탐색을 집중하기 때문에, 길찾기나 게임 AI처럼 출발점과 목적지가 명확한 single pair 문제에서 dijkstra보다 빠르게 동작한다.

---
