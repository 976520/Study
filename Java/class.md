## Java의 시작과 끝

Class에 대한 원론적인 설명은 [여기](https://github.com/976520/TIL/blob/main/Java/Object%20Oriented%20Programming/%EA%B0%9C%EB%85%90.md)로 redirect 하겠다...

1. class 선언

   `<접근 지정자> class <class명> {}`을 통해 다음과 같이 class를 생성할 수 있다. 이때 class명에는 다음과 같은 작성 조건이 존재한다. 이 때 중괄호를 통해 class 선어의 시작과 끝을 명시한다.

   1. 하나 이상의 문자로 이루어져야 한다.

   2. 첫 번째 글자는 숫자가 올 수 없다.

   3. $(달러사인), \_(언더바) 이외의 특수문자는 사용할 수 없다.

   4. Java의 예약어는 사용할 수 없다.

   Class명을 한글로 작성하여도 무관하며, 영문으로 작성할 시 대소문자를 구분한다. 첫 글자를 대문자로 작성하는 것이 관례이다.

   ```java
   public class Object {

   }

   class BrotherOfObject {

   }
   ```

   Java에서는 항상 **class명과 소스 파일명이 동일**하다. 위와 같은 경우 파일명이 `Object.java`가 되어야 한다. 소스 파일 역시 대소문자를 구분하므로 주의해야 한다. 일반적으로 소스 파일 하나당 class 하나를 생성하지만, 그 이상의 class 생성이 불가능하지는 않다. 소스 파일은 class의 선언을 담고 있을 뿐, class 자체와는 구분되는 개념이다. 따라서 위와 같은 코드를 컴파일하면 `Object.class`와 `BrotherOfObject.class`가 각각 생성된다. 하지만 **소스 파일명과 동일한 이름의 class만 접근 제한자를 `public`으로 설정**할 수 있다.

1. instance 생성

   또한 다음과 같이 class로부터 객체를 생성할 수 있다.

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

   이 코드가 실행되면 메모리에 class 변수와 객체가 생성된다. `Object` class는 하나지만, `new` 키워드를 사용한 만큼 객체가 메모리상에 새로 생성되며, 같은 class를 통해 생성되었지만 각각의 Object 객체는 자신만의 고유 데이터를 가진다. 또한 각 변수가 참조하는 `Object` 객체는 각각 완전히 독립된 서로 다른 객체이다.

1. class의 구분

   Class는 용도에 따라 다음 두 종류로 나뉜다.

   1. 라이브러리(API) class

      라이브러리 class는 다른 class에서 이용될 목적으로 설계된다. 만일 코드 전체어서 사용되는 class가 100개라면 그 중 99개는 라이브러리 class에 해당한다. 앞선 예제에서 `Object`는 라이브러리 class에 해당한다.

   2. 실행 class

      코드에서 오직 1개만 존재해야 하는 실행 class는 java 코드의 실행 진입점인 `main()` method를 제공하는 역할을 한다. `MakingInstance`는 실행 class에 해당한다.

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

   코드가 단일 class로 구성된다면 위와 같이 작성하는 것이 간단하고 좋을 수 있지만, ~~그럴거면 C++ 하세요~~ 대부분 OOP가 잘 적용된 코드에서는 라이브러리와 실행 class가 분리되어 있다.

---
