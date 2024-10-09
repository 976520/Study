# Java의 시작과 끝

Class에 대한 원론적인 설명은 [여기](https://github.com/976520/TIL/blob/main/Java/Object%20Oriented%20Programming/%EA%B0%9C%EB%85%90.md)로 redirect 하겠다. 이 글은 독자가 [OOP](https://github.com/976520/TIL/tree/main/Java/Object%20Oriented%20Programming)에 대한 기초적인 이해가 있다는 가정 하에 작성되었다. 따라서 OOP의 개념을 java에서 심층적으로 활용하는 방향으로 서술한다.

---

## class 선언

1. 문법

   `(접근 지정자) class [class명] {}`을 통해 같이 class를 생성할 수 있다. 중괄호를 통해 class 선어의 시작과 끝을 명시한다. 이때 class명에는 다음과 같은 작성 조건이 존재한다.

   1. 하나 이상의 문자로 이루어져야 한다.

   2. 첫 번째 글자는 숫자가 올 수 없다.

   3. $(달러사인), \_(언더바) 이외의 특수문자는 사용할 수 없다.

   4. Java의 예약어는 사용할 수 없다.

   Class명을 한글로 작성하여도 무관하며, 영문으로 작성할 시 대소문자를 구분한다. 첫 글자를 대문자로 작성하고, 여러 단어가 혼합된 이름이라면 뒤이어 오는 단어의 첫 글자를 대문자로 작성하는 pascal case를 쓰는 것이 관례이다.

   또한 접근 지정자(access modifier)에는 다음과 같은 종류가 있다.

   1. `public`

      Class의 외부에서 사용 가능하도록 노출시킨다. 한마디로 어디서든 접근할 수 있다.

   2. `protected`

      다른 class에게는 노출하지 않지만 동일 패키지 내의 class나, 상속받은 하위 class에게는 노출한다. 다른 패키지의 class에게는 노출되지 않는다.

   3. `default`

      `protected`와 동일하게 동일 패키지 내의 class에게 노출한다. 그러나 하위 class에게 노출하지 않는다.

   4. `private`

      클래스의 내부에서만 사용하며 외부로 노출하지 않는다.

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
