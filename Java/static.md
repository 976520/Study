## 정적이 흐르고

> static 멤버는 객체를 생성하지 않고 사용할 수 있는 field와 method를 뜻한다.

이들을 각각 static field와 static method라고 부른다.

1. 이해

   Static 멤버는 class로부터 생성된 instance에 소속된 멤버가 아니라, class에 직접 소속된 멤버이기 때문에 class 멤버라고 부르기도 한다. 이는 모든 instance가 공유하는 멤버로, 메모리 사용을 절약하고 데이터 일관성을 유지하는 데 유리하다.

   Static 멤버는 class에 고정된 멤버로서, class가 메모리에 로드될 때 함께 로드된다. 따라서 instance가 생성되지 않아도 사용할 수 있다.

   Field를 새로 만들 때 instance field로 선언할 것인가, static field로 선언할 것인가를 고민할 상황이 생길 것이다. 만약 객체마다 가지고 있어야 할 데이터라면 instance field로 선언하고, 그럴 필요 없이 class 내부에서 공용적으로 사용되는 데이터라면 static field로 선언하는 것이 좋다.

   Method의 경우에는 보다 단순하게 instance field를 이용하여 실행해야 한다면 instance method로, 그렇지 않는다면 static method로 선언한다. static method는 instance와 무관하게 동작하며, 주로 utility 함수나 공용 기능을 구현할 때 사용된다.

2. 문법

   `static [type] [field명](= 초기값)`을 통해 static field를 선언할 수 있으며, 이와 유사하게 `static [return type] [method명]((params)) { }`을 통해 static method를 선언할 수 있다.

   Class가 메모리 상에 load 될 시, static 멤버를 사용할 수 있다. 이에 접근하기 위해 일반적인 field와 method에 접근할 때와 같이 class명에 .(마침표)를 사용한다. 예를 들어, `ClassName.staticField` 또는 `ClassName.staticMethod()`와 같이 사용한다.

   static method는 class가 메모리에 올라갈 때 함께 로드되며, instance가 없어도 호출할 수 있다. 이는 주로 공용 기능이나 유틸리티 함수를 구현할 때 유용하다.

3. 초기화

   static 멤버는 class가 메모리에 로드될 때 초기화된다. static block을 사용하여 복잡한 초기화 로직을 구현할 수 있다.

   ```java
   public class MyClass {
       static int staticField;
       static {
           staticField = 10;
       }
   }
   ```

   static block은 class가 처음 로드될 때 한 번만 실행되며, 주로 static field의 초기화에 사용된다.
