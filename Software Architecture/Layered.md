## Layered pattern

1. 이해

   <img src="https://github.com/user-attachments/assets/3a06d85a-4a94-48a9-81da-7dfe33d81efe" width="70%" />

   Layered pattern은 system을 여러 계층으로 나누어 각 계층이 separation of concerns(관심사의 분리)를 달성하기 위해 특정 기능을 수행하도록 하는 architecture이다. 이러한 구조는 각 계층이 다른 계층과 통신하는 방식으로 작동한다.

   각 계층은 각자의 역할, 즉 자신의 책임에 해당하는 행위만을 수행하도록 분리되어야 한다. Layered architecture에서는 하위 계층에 의존적인 구조이다. 그러나 하위 계층은 상위 계층에 대한 정보를 가지고 있으면 안된다.

   예를 들어 user의 request를 받아 처리하는 presentation layer는 내부 business logic을 수행하는 application layer를 의존한다. 이때 하위 계층인 application layer는 상위 계층인 presentation layer에 대해 몰라야 한다.

---
