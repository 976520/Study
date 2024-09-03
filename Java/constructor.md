## constructor(생성자)

> constructor는 객체 생성 시 초기화를 하는 역할을 한다.

1. 이해

   Constructor는 `new`와 같이 사용되며 class로부터 객체를 생성할 때 호출되어 객체의 초기화를 담당하게 된다. 이때 초기화란, field를 초기화하거나, method를 호출하여 객체를 사용할 준비를 하는 것이다.

   이 constructor 없이는 class로부터 객체를 생성할 수 없다. `new`에 의해 constructor가 성공적으로 실행된다면, heap 영역에 객체가 생성되고, 그 주소가 반환된다. constructor 실행 중 에러가 발생한다면, 객체는 생성되지 않는다. 객체의 주소는 class type 변수에 저장되어 객체에 접근할 때 이용한다.

---
