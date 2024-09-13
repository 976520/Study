## 정적이 흐르고

> static 멤버는 class에 고정된 멤버로서, 객체를 생성하지 않고 사용할 수 있는 filed와 method를 뜻한다.

이들을 각각 static filed와 static method라고 부른다.

1. 이해

   정적 멤버는 class로부터 생성된 instance에 소속된 멤버가 아니라, class에 직접 소속된 멤버이기 때문에 class 멤버라고 부르기도 한다.

   Field를 새로 만들 때 instance field로 선언할 것인가, static field로 선언할 것인가를 고민할 상황이 생길 것이다. 만약 객체마다 가지고 있어야 할 데이터라면 instance field로 선언하고, 그럴 필요 없이 class 내부에서 공용적으로 사용되는 데이터라면 static field로 선언하는 것이 좋다.

   Method의 경우에는 보다 단순하게 instance field를 이용하여 실행해야 한다면 instance method로, 그렇지 않는다면 static method로 선언한다.

2. 문법

   `static [type] [field명](= 초기값)`을 통해 static field를 선언할 수 있으며, 이와 유사하게 `static [return type] [method명]((params)) { }`을 통해 static method를 선언할 수 있다.

3. 사용

4. 초기화
