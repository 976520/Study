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

   7. 소멸
