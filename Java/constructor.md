## 생성자

> constructor(생성자)는 객체 생성 시 초기화를 하는 역할을 한다.

1. 이해

   Constructor는 `new`와 같이 사용되며 class로부터 객체를 생성할 때 호출되어 객체의 초기화를 담당하게 된다. 이때 초기화란, field를 초기화하거나, method를 호출하여 객체를 사용할 준비를 하는 것이다.

   이 constructor 없이는 class로부터 객체를 생성할 수 없다. `new`에 의해 constructor가 성공적으로 실행된다면, heap 영역에 객체가 생성되고, 그 주소가 반환된다. constructor 실행 중 에러가 발생한다면, 객체는 생성되지 않는다. 객체의 주소는 class type 변수에 저장되어 객체에 접근할 때 이용한다.

2. default constructor

   모든 class는 constructor가 반드시 하나 이상 존재해야 한다. class를 설계할 때 constructor 선언을 생략했다면,

   ```java
    class Example() {

    }
   ```

   컴파일러가 자동으로 중괄호 블럭 내부가 비어 있는 default constructor를 추가한다.

   ```java
    class Example() {
      Example() {} // <- 컴파일 과정에서 자동으로 추가
    }
   ```

   또한 class가 `public`으로 선언된다면,

   ```java
    public class Example() {

    }
   ```

   default constructor에도 `public`이 붙게 된다.

   ```java
    public class Example() {
      public Example() {} // <- 컴파일 과정에서 자동으로 추가
    }
   ```

   `public` 없이 선언되었다면 default constructor에는 붙지 않는다.

   Class에서 constructor를 따로 선언하지 않아도 다음과 같이 `new` 키워드 뒤에 default constructor를 호출하여 instance를 생성할 수 있다. 다음과 같은 경우 `Gay()`가 default constructor에 해당하며, 이를 이용하여 객체를 생성한 모습이다.

   ```java
   class Gay() {
     Gay 황지훈 = new Gay();
   }
   ```

   Class 내부에 명시적으로 선언된 constructor가 하나라도 있다면 컴파일러는 default constructor를 생성하지 않기 때문에, 객체를 다양하게 초기화하기 위해서는 constructor를 명시적으로 선언하는 것이 좋다.

3. 문법

   생성자를 명시적으로 선언하려면 class 내부에 `[class명]((params)) {}`와 같이 작성하면 된다. 얼핏 보면 method와 비슷하게 보이나, method와 달리 return type이 없고 class명과 동일한 이름을 가진다. Constructor의 중괄호 블럭 내부에는 **객체의 초기화 코드**가 작성된다. 매개변수 선언의 경우에는 method와 비슷하게 생략할 수 있고, 다수를 선언할 수도 있다. 이때 매개변수는 `new`로 constructor를 호출할 때 외부의 값을 constructor 블록 내부로 가져오는 역할을 한다.

4. 사용

   다음은 두 parameter들을 받는 constructor를 선언한 코드이다.

   ```java
   public class Gay() {
      Gay(String name, int height) {

      }
   }
   ```

   이렇게 선언된 `Gay()` constructor를 호출하여 객체를 생성하는 코드는 다음과 같다.

   ```java
   public class StudentsInClass4() {
     public static void main(String[] args) {
       Gay 황지훈 = new Gay("황지훈", 158)
       Gay 이주언 = new Gay("이주언", 170)
     }
   }
   ```

---
