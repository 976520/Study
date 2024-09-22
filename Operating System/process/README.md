# Kim Ximya X D.Sanders - Process <-- 명곡추

> Process는 실행 중인 program을 의미한다.

초기의 computer system은 batch processing(일괄 처리) 방식을 사용했기 때문에, 한 번에 오직 하나의 작업(job)만을 처리할 수 있었다. 실행 중인 단 하나의 program이 system 전체를 완전히 제어하고, 모든 system 자원에 자유롭게 접근할 수 있었다. 이후에는 여러 program이나 작업을 동시에 실행할 수 있는 시분할(time-sharing) system이 등장했다.

그러나 현재의 computer system에서는 메모리에 다수의 program을 동시에 적재하고 이들을 병행적으로 실행하는 것이 가능해졌다. 이러한 변화로 인해 다양한 program들을 보다 효율적으로 제어하고 관리할 수 있는 방법이 필요하게 되었다.

단일 사용자 system에서도 여러 program을 동시에 실행할 수 있는 것이 가능해졌다. 또한 multi tasking을 지원하지 않는 imbedded 장치처럼 한 번에 하나의 program만 실행할 수 있더라도, OS는 memory 관리와 같은 내부 활동을 지원해야 하는 경우가 있다.

---

## 이해

Process는 현대의 computer system에서 작업의 단위를 의미한다.

OS는 각각의 program을 독립적인 공간에 적재하고, 이를 위해 각각의 program에 대한 독립적인 memory 영역을 제공하는 방법을 사용한다. 이러한 각각의 독립적인 memory 영역을 가지는 program을 process라고 한다.

OS가 복잡해질수록, 사용자를 위해 더 많은 기능을 제공한다. 예를 들어 하나의 system은 일부는 사용자에게 직접적으로 제공되는 서비스를 제공하고, 일부는 kernel에서 작업을 처리하는 process들로 구성된다. 이 process들은 병행 실행이 가능하며, CPU는 이 process 간에서 multiplex(다중화)된다.

## program과의 관계

Program은 명령어 list를 내용으로 가진 파일(실행 파일)이며, passive entity(수동적인 존재)이다. 반면에 process는 다음에 실행할 명령어를 지정하는 program counter와 관련 resource 등을 가진 active entity(능동적인 존재)이다. 실행 파일이 memory에 올라가면, program은 process가 된다.

동일한 program이 여러 개의 process로 실행될 수 있다. 이때 각각의 process는 독립적인 memory 영역을 가지며, 서로 다른 작업을 동시에 수행할 수 있다. 예를 들어 우리가 chrome을 여러 번 실행하면 이들은 tab으로 분리되어 별도의 process로 간주된다.

Process가 다른 개체를 위한 실행 환경이 될 수 있다. 예를 들어 JVM(Java Virtual Machine)은 java program을 실행하는 환경을 제공하는데, 이때 JVM 자체는 하나의 process이다.

---
