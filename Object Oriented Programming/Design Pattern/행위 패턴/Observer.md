## 옵저버

1. 이해

   Observer pattern은 observer(관찰자)와 subject(대상자)로 이루어진다. Observer는 subject를 관찰하고, subject는 변화가 있을 때 마다 observer에게 전달한다. Observer pattern은 일대다(one-to-many) 의존성을 가지며, 한 subject에 여러 observer가 있을 수 있다. Pub/Sub pattern이라고도 한다.

   사실 observer가 관찰하기보다는 갱신을 위한 data를 전달 받기를 기다리고 있다고 보는 것이 정확하다.

2. 사용
