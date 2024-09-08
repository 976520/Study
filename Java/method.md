## 메소드 연기

> method는 객체의 동작을 실행하는 역할을 한다.

Method에 대한 원론적인 설명은 [여기](https://github.com/976520/TIL/blob/main/Java/Object%20Oriented%20Programming/%EA%B0%9C%EB%85%90.md)로 redirect 하겠다.

---

1. 이해

   Java에서 method는 객체의 동작에 해당하는 중괄호 블록을 뜻한다. Method는 field에 접근하여 읽고 수정하는 역할도 하지만, 다른 객체를 생성하여 여러 기능을 수행하기도 한다. 이 method는 객체 간의 데이터를 전달하는 수단으로 이용된다.

   마치 다른 언어의 함수 처럼 method를 호출하면, 그 안의 모든 코드를 일괄적으로 실행한다. 외부로부터 parameter를 받을 수 있고, 동작 실행 이후 어떠한 값을 return할 수 있다.

2. 문법

   `[return type] [method명] (([params])) {}`을 통해 method를 만들 수 있다. 이 때 중괄호를 제외한 부분을 선언부 혹은 method signature라고 부른다.

   `[return type]`을 통해 method가 return하는 반환값의 type을 명시할 수 있다. 또한 method명에 후행하는 소괄호 내부에 method의 parameter들을 선언할 수 있다.

3. 사용
