# JVM

> Java 실행을 위한 가상 기계.

1. 이해

   Java code를 compile하면 `.class` 확장자를 가진 java byte code가 생성된다. 이 java byte code를 JVM이 해석하여 실행한다. 만약 `hello.java`가 있는 위치에서 다음 명령어를 실행하면,

   ```shell
   javac hello.java
   ```

   해당 위치에 `hello.class` 파일이 생성된다.

   ```shell
   java hello
   ```

   를 통해 `hello.class` 파일을 실행할 수 있다.

   Java는 OS에 종속되지 않고, 아무 OS 환경에서나 동일하게 실행할 수 있다는 장점이 있다. 이때 OS 위에서 CPU가 java를 인식하고 실행하도록 하는 것이 JVM이다.

1. byte code

   위에서 `.class` 파일이 byte code라고 했는데, byte code는 컴퓨터가 직접 실행하는 binary code가 아닌 가상 머신이 이해할 수 있는 중간 단계의 code이다. 이 byte code는 플랫폼에 독립적이라 어떤 OS에서든 해당 OS의 JVM만 있다면 실행이 가능하다.

   Java의 경우 `.java` 파일을 compile하면 JVM이 이해할 수 있는 byte code인 `.class` 파일이 생성된다.

1. JIT(Just-In-Time) compiler

   > JIT compiler는 byte code를 binary code로 변환하여 실행한다.

   이 과정을 JIT compilation 또는 dynamic translation이라고 한다.

1. 특징

   1. Stack 기반

   2. 단일 상속 형태의 객체 지향 프로그래밍을 가상 머신 수준에서 구현

   3. Pointer 지원

      C처럼 주소 값 조작이 가능한 pointer 연산은 불가

   4. Garbage Collection

   5. 명시적인 type 정의

      이로써 platform-independent한 program을 만들 수 있다

   6. Data flow analysis 기반 byte code verifier

   7. 다음 명령어에 stack에서 가져올 피연산자의 type 지정

---
