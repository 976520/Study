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

   JVM은 이 뿐만 아니라 memory management, garbage collection 등의 기능을 제공한다.

1. byte code

   위에서 `.class` 파일이 byte code라고 했는데, byte code는 컴퓨터가 직접 실행하는 binary code가 아닌 가상 머신이 이해할 수 있는 중간 단계의 code이다. 이 byte code는 플랫폼에 독립적이라 어떤 OS에서든 해당 OS의 JVM만 있다면 실행이 가능하다.

   Java의 경우 `.java` 파일을 compile하면 JVM이 이해할 수 있는 byte code인 `.class` 파일이 생성된다.

1. JIT(Just-In-Time) compiler

   JIT는 프로그램을 실행하기 전에 한 번에 compile하는 것이 아니라, 프로그램을 실행하는 시점에서 필요한 부분만 compile하는 방식이다. 이 과정을 JIT compilation 또는 dynamic translation이라고 한다. JVM의 JIT compiler는 byte code를 binary code로 변환하여 실행한다.

   필요한 부분을 한 줄씩 읽는 interpreter 방식과 비슷하지만, JIT는 interpreter와 달리 자주 실행되는 부분을 cache하여 다음 실행 시 빠르게 실행할 수 있다는 차이가 있다. JVM의 경우 code cache라는 공간에 자주 실행되는 부분을 binary code로 저장한다.

1. 특징

   1. Stack 기반

   2. 단일 상속 형태의 객체 지향 프로그래밍을 가상 머신 수준에서 구현

   3. Reference(참조) 지원

      Reference는 C나 C++의 Pointer와 동일하게 주소를 통해 원본 data에 접근할 수 있다.

      Pointer는 저수준 언어의 특성으로서 memory를 아얘 조작할 수 있다. 이는 성능에 도움이 될 지는 몰라도 segment fault를 발생시킬 가능성이 있어서 안전하지 않다.

      때문에 java의 reference는 memory의 직접적인 접근을 제한하여 안정성을 챙겼다고 할 수 있다. 이는 후술할 Garbage Collection에서 중요한 역할을 한다.

   4. Garbage Collection

      1. 이해

         > Garbage collection은 더이상 사용되지 않는 memory 영역을 자동으로 찾아 제거하는 기능이다.

         JVM의 heap에서 동적으로 할당된 memory 중 쓸모없는 memory object(garbage)를 찾아 주기적으로 해제하는 process라고 할 수 있다. C나 C++의 경우~~에만~~ 이런 기능이 없어서 개발자가 수동으로 memory를 할당하고 해제해야 한다.

         ```c
         void main() {
            int* dontHaveGC = (int*)malloc(sizeof(int));
            *dontHaveGC = 10;
            free(dontHaveGC);
            dontHaveGC = NULL;
         }
         ```

         반면 java에서는 GC가 이를 자동으로 처리하기 때문에, memory 자원을 더 효율적으로 사용할 수 있고, memory leak(누수) issue에 대해 신경쓰지 않아도 된다는 장점이 있다. 아래 코드에서는 `haveGC` 변수가 `null`로써 더 이상 참조되지 않으면, garbage로 간주하고 GC가 자동으로 메모리를 해제한다.

         ```java
         public class JavaHaveGC {
            public static void main(String[] args) {
               Integer haveGC = new Integer(10);
               haveGC = null;
            }
         }
         ```

      2. Garbage의 조건

         GC는 object를 reachability~~도달가능미~~에 따라, object에게 유효한 reference가 있다면 reachable, 그렇지 않다면 unreachable로 구분한다.

         <img src="https://github.com/user-attachments/assets/862bcd65-1262-4409-bbe7-23fa08741c6d" width="450">

         Heap 위의 object가 사용중이라면, 직접 가져다 쓸 수는 없기에 그 object를 사용하는 코드가 있는 곳에서 그 object를 참조하는 reference가 있을 것이다. 이때 그 object는 reachable이라고 할 수 있다.

      3. Stop The World

         > JVM이 GC가 수행되는 동안 모든 thread를 멈추는 것을 STW(Stop The World)라고 한다.

         GC관련 thread를 제외한 모든 thread의 연산이 정지하기~~로드롤러다~~ 때문에 GC가 너무 자주 실행되면 처리 시간이 오래 걸리는 문제가 생긴다. 이제는 사장된 인터넷 익스플로러가 대표적인 예시이다.

   5. 명시적인 type 정의

      이로써 platform-independent한 program을 만들 수 있다

   6. Data flow analysis 기반 byte code verifier

   7. 다음 명령어에 stack에서 가져올 피연산자의 type 지정

---
