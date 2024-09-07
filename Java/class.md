# Java의 시작과 끝

Class에 대한 원론적인 설명은 [여기](https://github.com/976520/TIL/blob/main/Java/Object%20Oriented%20Programming/%EA%B0%9C%EB%85%90.md)로 redirect 하겠다. 이 글은 독자가 [OOP](https://github.com/976520/TIL/tree/main/Java/Object%20Oriented%20Programming)에 대한 기초적인 이해가 있다는 가정 하에 작성되었다. 따라서 OOP의 개념을 java에서 심층적으로 활용하는 방향으로 서술한다.

---

## class 선언

1. 문법

   `(접근 지정자) class [class명] {}`을 통해 같이 class를 생성할 수 있다. 이때 class명에는 다음과 같은 작성 조건이 존재한다. 이 때 중괄호를 통해 class 선어의 시작과 끝을 명시한다.

   1. 하나 이상의 문자로 이루어져야 한다.

   2. 첫 번째 글자는 숫자가 올 수 없다.

   3. $(달러사인), \_(언더바) 이외의 특수문자는 사용할 수 없다.

   4. Java의 예약어는 사용할 수 없다.

   Class명을 한글로 작성하여도 무관하며, 영문으로 작성할 시 대소문자를 구분한다. 첫 글자를 대문자로 작성하는 것이 관례이다.

2. 사용

   다음과 같이 class를 선언할 수 있다.

   ```java
   public class Object {

   }

   class BrotherOfObject {

   }
   ```

3. class와 파일명

   Java에서는 항상 **class명과 소스 파일명이 동일**하다. 위와 같은 경우 파일명이 `Object.java`가 되어야 한다. 소스 파일 역시 대소문자를 구분하므로 주의해야 한다. 일반적으로 소스 파일 하나당 class 하나를 생성하지만, 그 이상의 class 생성이 불가능하지는 않다. 소스 파일은 class의 선언을 담고 있을 뿐, class 자체와는 구분되는 개념이다. 따라서 위와 같은 코드를 컴파일하면 `Object.class`와 `BrotherOfObject.class`가 각각 생성된다. 하지만 **소스 파일명과 동일한 이름의 class만 접근 제한자를 `public`으로 설정**할 수 있다.

---

## instance 생성

1. 문법

   `[class명] [변수명] = new [class명]`을 통해 class를 참조하여 새로운 instance를 생성할 수 있다.

2. 사용

   다음과 같이 class로부터 객체를 생성할 수 있다.

   ```java

   public class MakingInstance {
   public static void main(String[] args) {
      Object firstObject = new Object();
      System.out.println("firstObject 변수가 Object 객체를 참조");

      Object secondObject = new Object();
      System.out.println("secondObject 변수가 또 다른 Object 객체를 참조");
   }
   }
   ```

3. instance와 메모리

   위 코드를 실행하면 메모리상에 class 변수와 객체가 생성된다. `Object` class는 하나지만, `new` 키워드를 사용한 만큼 객체가 메모리상에 새로 생성되며, 같은 class를 통해 생성되었지만 각각의 Object 객체는 자신만의 고유 데이터를 가진다. 또한 각 변수가 참조하는 `Object` 객체는 각각 완전히 독립된 서로 다른 객체이다.

---

## class의 구분

1. 이해

   Class는 용도에 따라 다음 두 종류로 나뉜다.

   1. 라이브러리(API) class

   라이브러리 class는 다른 class에서 이용될 목적으로 설계된다. 만일 코드 전체어서 사용되는 class가 100개라면 그 중 99개는 라이브러리 class에 해당한다. 앞선 예제에서 `Object`는 라이브러리 class에 해당한다.

   2. 실행 class

   코드에서 오직 1개만 존재해야 하는 실행 class는 java 코드의 실행 진입점인 `main()` method를 제공하는 역할을 한다. `MakingInstance`는 실행 class에 해당한다.

2. 사용

   앞선 예제의 `Object` 안에 `main()` method를 작성하여 라이브러리 class인 동시에 실행 class인 class를 만들 수도 있다.

   ```java
   public class Object {

   // 귀찮아서 안 썼지만, 라이브러리 class로서의 코드가 여기에 있을 수 있다.

   // 동시에 실행을 위한 main() method도 있을 수 있다.
   Public static void main(String[] args) {
      Object firstObject = new Object();
      System.out.println("firstObject 변수가 Object 객체를 참조");

      Object secondObject = new Object();
      System.out.println("secondObject 변수가 또 다른 Object 객체를 참조");
   }
   }
   ```

   코드가 단일 class로 구성된다면 이와 같이 작성하는 것이 간단하고 좋을 수 있지만, ~~그럴거면 C++ 하세요~~ 라이브러리와 실행 class가 분리된 코드가 유지보수성에서 우수하며, OOP를 더 적절히 적용했다고 볼 수 있다.

---

## field

1. 문법

   `[type] [필드명] (= 초기값);`을 통해 선언할 수 있다. 이 field의 선언은 class의 중괄호 내부 어디서든 존재할 수 있다.

   `[type]`을 통해 field에 저장할 데이터의 종류를 결정할 수 있다. `int`, `float` 등의 기본 type과 배열, class, interface 등의 참조 type이 모두 올 수 있다.

   또한 초기값을 생략할 수 있으며, 초기값이 주어지지 않은 field는 객체 생성 시 기본 초기값으로 설정되게 된다. 이 때 field의 type에 따라 설정되는 초기값이 다르며, 다음은 type이 기본 type일 때 각각의 자료형에 대해 설정되는 초기값을 나열한 것이다.

   1. `byte` `short` `int` 0
   2. `char` \u0000 (공백)
   3. `long` 0L
   4. `float` 0.0F
   5. `double` 0.0
   6. `boolean` false

   참조 type일 때는 `null`값으로 초기화 된다.

2. 이해

   > 객체의 데이터를 저장하는 역할을 한다.

   여기서 데이터란, 객체의 고유 데이터 뿐만 아니라 객체의 부품 객체, state 등을 모두 포괄한다. 이주언 객체를 예로 들면 이름과 성별은 고유 데이터에 해당하고, 학교와 학번, 게이 여부는 state에 해당한다. 그리고 머리와 몇 없는 머리카락 등은 부품에 해당할 것이다. 따라서 이주언 class를 설계할 때 이 데이터들을 field로 선언해야 한다.

3. 사용

   Field를 사용하는 것은 단순히 field값을 읽고, 변경하는 작업을 뜻한다. 아래는 이주언 class를 알맞은 field의 선언과 함께 설계한 모습이다.

   ```java
   public class 이주언 {
      String name = "이주언";
      String sex = "male";

      String school = "광주소프트웨어마이스터고등학교";
      int number = 1414;
      boolean isGay;

      Head head = new Head;
      Hair hair = new Hair;

      void 탈모() {
         hear = null;
      }
   }
   ```

   Class 내부의 method에서 field에 접근할 경우 단순히 field의 이름으로 읽고 변경할 수 있다. 위 코드에서는 `탈모()` method 안에서 `hear` field의 값을 `null`로 변경하였다.

   하지만 class 외부에서 사용할 경우 우선적으로 class로부터 instance를 생성한 뒤 field를 사용해야 한다. Field는 객체에 소속된 데이터이므로, 객체가 없으면 field도 없기 때문이다.

   ```java
   public class 황지훈 {

      이주언 girlfriend = new 이주언;
      girlfriend.isGay = true;

      void 중성화() {
         girlfriend.sex = "female"
         girlfriend.isGay = false;
      }

      System.out.println("now, 이주언's sex is" + girlfriend.sex);
   }

   // 출력: now, 이주언's sex is female
   ```

   위 코드에서는 이주언 class의 field를 외부에서 변경하기 위해 `girlfriend` 변수를 통해 class를 참조하고, .(도트) 연산자를 통해 field에 접근하였다.

4. 변수와의 차이

   선언 형태는 일반적인 변수와 비슷할지라도 각각 구분된 개념이다. 그래서 혹자는 field를 class 멤버 변수라고 칭하기도 한다. 객체에 내부의 변수는 constructor 혹은 method 안에서만 사용되며, 이들이 종료되면 자동으로 소멸하게 된다. 하지만 field는 constructor와 method 전체에서 사용되며, 객체가 소멸되지 않는 한 계속 존재한다.

---

## method

> method는 객체의 동작을 실행하는 역할을 한다.

---

## constructor(생성자)

> constructor는 객체 생성 시 초기화하는 역할을 한다.

---
