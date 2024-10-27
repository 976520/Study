# Kim Ximya X D.Sanders - Process <-- 명곡추

> Process는 실행 중인 program을 의미한다.

## 이해

1. 등장 배경

   초기의 computer system은 batch processing(일괄 처리) 방식을 사용했기 때문에, 한 번에 오직 하나의 작업(job)만을 처리할 수 있었다. 실행 중인 단 하나의 program이 system 전체를 완전히 제어하고, 모든 system 자원에 자유롭게 접근할 수 있었다. 이후에는 여러 program이나 작업을 동시에 실행할 수 있는 시분할(time-sharing) system이 등장했다.

   그러나 현재의 computer system에서는 메모리에 다수의 program을 동시에 적재하고 이들을 병행적으로 실행하는 것이 가능해졌다. 이러한 변화로 인해 다양한 program들을 보다 효율적으로 제어하고 관리할 수 있는 방법이 필요하게 되었다.

   단일 사용자 system에서도 여러 program을 동시에 실행할 수 있는 것이 가능해졌다. 또한 multi tasking을 지원하지 않는 imbedded 장치처럼 한 번에 하나의 program만 실행할 수 있더라도, OS는 memory 관리와 같은 내부 활동을 지원해야 하는 경우가 있다.

2. 개념

   Process는 현대의 computer system에서 작업의 단위를 의미한다.

   OS는 각각의 program을 독립적인 공간에 적재하고, 이를 위해 각각의 program에 대한 독립적인 memory 영역을 제공하는 방법을 사용한다. 이러한 각각의 독립적인 memory 영역을 가지는 program을 process라고 한다.

   OS가 복잡해질수록, 사용자를 위해 더 많은 기능을 제공한다. 예를 들어 하나의 system은 일부는 사용자에게 직접적으로 제공되는 서비스를 제공하고, 일부는 kernel에서 작업을 처리하는 process들로 구성된다. 이 process들은 병행 실행이 가능하며, CPU는 이 process 간에서 multiplex(다중화)된다.

3. section

   <img src="https://github.com/user-attachments/assets/aa4a0cb0-e4f0-4d05-874d-72e19ba74828" width="180">

   Process는 여러 section으로 구성되어 memory에 적재된다. 이 section들은 각각 다른 목적을 가지며, 이를 통해 program의 구조를 더 효율적으로 관리할 수 있다. Section의 종류는 다음과 같다.

   1. text section(code section)

      program의 **소스 코드**가 저장되는 영역이다. 실행 가능한 기계어 코드를 포함한다.

   2. data section

      **전역 변수**, 정적 변수, 상수 등이 저장되는 영역이다. program의 실행 중에 변경 가능한 데이터를 포함한다.

   3. stack section

      **함수 호출 시 임시로 사용**되는 데이터를 저장하는 영역이다. 함수 호출과 관련된 지역 변수, 매개변수, 반환 주소, 복귀 주소 등이 저장된다.

   4. heap section

      동적 메모리 할당을 위한 영역이다. program이 **실행 중에 동적으로 할당**되는 데이터를 저장한다.

---
