## section

<img src="https://github.com/user-attachments/assets/aa4a0cb0-e4f0-4d05-874d-72e19ba74828" width="180">

Process는 여러 section으로 구성되어 memory에 적재된다. 이 section들은 각각 다른 목적을 가지며, 이를 통해 program의 구조를 더 효율적으로 관리할 수 있다. Section의 종류는 다음과 같다.

1.  text section

    program의 **소스 코드**가 저장되는 영역이다. 실행 가능한 기계어 코드를 포함한다.

2.  data section

    **전역 변수**, 정적 변수, 상수 등이 저장되는 영역이다. program의 실행 중에 변경 가능한 데이터를 포함한다.

3.  stack section

    **함수 호출 시 임시로 사용**되는 데이터를 저장하는 영역이다. 함수 호출과 관련된 지역 변수, 매개변수, 반환 주소, 복귀 주소 등이 저장된다.

4.  heap section

    동적 메모리 할당을 위한 영역이다. program이 **실행 중에 동적으로 할당**되는 데이터를 저장한다.

이때 text section과 data section은 크기가 고정되어 실행되는 동안 변경되지 않는다. 하지만 stack section과 heap section은 크기가 가변적이며, 실행 중에 크기가 동적으로 커지거나 줄어들 수 있다.

함수가 호출 될 때마다 매개변수, 지역 변수, 복귀 주소 등을 포함하는 activation record(활성화 레코드)가 stack에 push된다. 함수에서 제어가 복귀될 때 stack에서 activation record가 pop된다. Memory가 동적으로 할당됨에 따라 heap이 확장되고, memory가 system에 반환되면 heap이 축소된다. 이 stack과 heap이 서로의 방향으로 커지게 되는데, OS는 이들이 서로 겹치지 않도록 해야 한다.

---
