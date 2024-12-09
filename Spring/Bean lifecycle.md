## Bean의 인생

> Bean lifecycle은 bean이 생성되고 소멸되는 과정을 의미한다.

---

1. 이해

   Bean lifecycle의 대략적인 흐름은 다음과 같다.

   1. Spring Container 생성

   2. Bean 생성
   3. Dependency Injection

   4. 초기화 후 callback(init)

      Bean이 생성되고 DI를 받은 후 호출된다.

   5. 사용

   6. 소멸 전 callback(destroy)

      Bean이 소멸되기 직전에 호출된다.

   7. Spring 종료

2. Bean lifecycle callback

   DB연결, socket 연결 등 시작 시점에 완료되어야 하고, 종료 시점에 해제되어야 하는 경우, 이 callback을 통해 편리하게 구현할 수 있다. 따라서 callback들은 조건에 따라 호출되지 않을 수 있다.

   Spring은 다음과 같은 방법을 통해 lifecycle callback을 제공한다.

   1. interface

      `InitializingBean`의 `afterPropertiesSet()` method를 통해 DI 완료 후 초기화를 진행할 수 있다. 또한 `DisposableBean`의 `destroy()` method를 통해 소멸 작업을 진행할 수 있다.

   2. annotation

      최신 spring에서 가장 권장하는 방법이다. `@PostConstruct`와 `@PreDestroy` annotation을 통해 초기화와 소멸 전 작업을 진행할 수 있다.

   3. config

      설정 정보에서 초기화와 소멸 전 method를 지정하는 방법이다. Spring 코드에 의존하지 않고 method명을 자유롭게 설정 할 수 있다.

      `@Bean` 지정 시 initMethod와 destroyMethod를 직접 지정해야 하기 때문에 좀 귀찮다.

---
