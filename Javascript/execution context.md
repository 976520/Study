# 실행 컨텍스트

> 실행 컨텍스트는 JS 코드를 실행하는데 필요한 환경을 제공하고 실행 결과를 관리하는 영역이다.

실행 컨텍스트는 다음과 같은 역할을 수행하는 매커니즘이다.

1. scope 관리

    - 모든 식별자의 scope를 구분하여 등록하고 식별자에 연결(binding)된 value의 변화를 관리한다.

    - scope chain을 형성하고, 이를 이용해 상위 scope로 이동하며 식별자를 찾는다.

2. 코드 순서(call stack) 관리

    - 실행 중인 코드의 실행 순서를 변경하거나 되돌아갈 수 있게 한다.

모든 코드는 컨텍스트를 통해 실행되고 관리된다.

---

## 소스코드 처리 방법

JS 엔진은 모든 소스코드를 아래 두 단계로 나누어 처리한다. ~~문서들에서 여러 용어가 혼용되니 잘 기억하자...~~

1. 소스코드 평가 = creation phase = Variable/Object/Function environment creation

    소스코드 평가 과정에서는 이 두 작업이 진행된다.

   - 실행 컨텍스트를 생성

   - 선언문 실행 -> 식별자를 실행 컨텍스트가 관리하는 scope에 등록하여 scope구성

2. 소스코드 실행 = execution phase = Execution context running = runtime

    평가 과정이 끝나면 남은 코드가 실제로 동작하는 단계이다.

    코드 실행에 필요한 정보는 scope에서 탐색하여 사용하고, 코드 실행 결과도 scope에 등록한다.

---

## 소스코드의 분류

ECMAScript 코드는 크게 4가지 타입으로 분류된다. 이 타입에 따라 실행 컨텍스트를 생성하는 과정과 관리 내용이 다르다.

- global code

  전역에 존재하는 코드이다. 전역에 정의된 함수, 클래스 내부의 코드는 포함되지 않는다.

- function code

  함수 내부에 존재하는 코드이다. 안에 중첩된 함수, 클래스 내부의 코드는 포함되지 않는다.

  function code는 local valuable, parameter, arguments object를 관리해야 하고, 이를 포함한 local scope를 생성하여 scope chain에 연결해야 한다.

- eval code

  `eval`함수에 인수로 전달되어 실행되는 코드인데, 이는 strict mode에서 독자적인 scope를 생성한다는 특징이 있다.

- module code

  모듈 내부에 존재하는 코드이며, 모듈별로 독립적인 module scope를 생성한다.

---

## call stack

> call stack은 JS 코드의 실행 순서를 관리하는 자료구조이다.

실행 컨텍스트 스택이라고 하기도 한다. 

<img width="400" height="536" alt="Image" src="https://github.com/user-attachments/assets/4b69ee44-f4d4-4084-9151-3be0f4052ed0" />

상술했듯 소스코드가 평가 과정을 거치면 실행 컨텍스트가 생성되는데, 이것이 call stack의 최상위에 push된다. 따라서 call stack의 top에 있는 실행 컨텍스트는 현재 실행중인 코드의 실행 컨텍스트라고 할 수 있다. 코드 실행이 끝나면 해당 컨텍스트는 pop되고, 다음 컨텍스트가 실행된다.
이 과정을 반복하다가 **전역 실행 컨텍스트(Global Execution Context)**가 pop되면 call stack 비게 되고 프로그램이 종료된다.

---