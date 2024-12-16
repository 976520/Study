# JVM

> Java 실행을 위한 가상 기계.

1. 이해

   Java code를 compile하면 bytecode가 생성된다. 이 bytecode를 JVM이 해석하여 실행한다.

   Java는 OS에 종속되지 않고, 아무 OS 환경에서나 동일하게 실행할 수 있다는 장점이 있다. 이때 OS 위에서 CPU가 java를 인식하고 실행하도록 하는 것이 JVM이다.

1. 특징

   1. Stack 기반

   2. 단일 상속 형태의 객체 지향 프로그래밍을 가상 머신 수준에서 구현

   3. Pointer 지원

      C처럼 주소 값 조작이 가능한 pointer 연산은 불가

   4. Garbage Collection

   5. 명시적인 type 정의

      이로써 platform-independent한 program을 만들 수 있다.|

   6. Data flow analysis 기반 byte code verifier

   7. 다음 명령어에 stack에서 가져올 피연산자의 type 지정

---
