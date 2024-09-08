## 메소드 연기

> method는 객체의 동작을 실행하는 역할을 한다.

Method에 대한 원론적인 설명은 [여기](https://github.com/976520/TIL/blob/main/Java/Object%20Oriented%20Programming/%EA%B0%9C%EB%85%90.md)로 redirect 하겠다.

---

1. 이해

   Java에서 method는 객체의 동작에 해당하는 중괄호 블록을 뜻한다. Method는 field에 접근하여 읽고 수정하는 역할도 하지만, 다른 객체를 생성하여 여러 기능을 수행하기도 한다. 이 method는 객체 간의 데이터를 전달하는 수단으로 이용된다.

   마치 다른 언어의 함수와 같이 method를 호출하면, 그 안의 모든 코드를 일괄적으로 실행한다. 외부로부터 매개변수를 받아 함수 내부에서 사용할 수 있고, `return`을 통해 동작 실행 이후 어떠한 값을 반환할 수 있다. 따라서 method 안에서 `return`이 실행될 시, method는 즉시 종료된다. 물론 매개변수와 반환값이 존재하지 않는 method도 있을 수 있다.

2. 문법

   `[return type] [method명] ((params)) {}`을 통해 method를 만들 수 있다. 이 때 중괄호를 제외한 부분을 선언부 혹은 method signature라고 부른다.

   `[return type]`을 통해 method가 return하는 반환값의 type을 명시할 수 있다. 또한 method명에 후행하는 소괄호 내부에 method의 매개변수들을 선언할 수 있다. 만일 반환값의 type이 `void`로 명시되어 있다면, 값을 반환하지 않는다는 뜻이다. 따라서 `return`은 반환값 없이 혼자 사용되며 method를 종료하는 역할만을 수행한다.

   Class처럼 method의 이름에도 작성 규칙이 있으며, 이는 다음과 같다.

   1. 하나 이상의 문자로 이루어져야 한다.

   2. 첫 번째 글자는 숫자가 올 수 없다.

   3. $(달러사인), \_(언더바) 이외의 특수문자는 사용할 수 없다.

   4. Java의 예약어는 사용할 수 없다.

   Method명을 한글로 작성하여도 무관하다. 영문으로 작성할 시 첫 글자를 소문자로 작성하고, 여러 단어가 혼합된 이름이라면 뒤이어 오는 단어의 첫 글자를 대문자로 작성하는 camel case를 쓰는 것이 관례이다. 또한 이름을 지을 때 각 method가 어떤 기능을 하는지 쉽게 알 수 있도록 기능의 이름을 사용하는 것이 좋다.

3. 사용

   Method는 호출에 의해 실행된다. Class 외부에서 호출할 경우 우선 class에서 객체를 생성한 뒤, 참조를 이용하여 method를 호출해야 한다. Method는 객체에 소속된 멤버이므로 객체가 없으면 method도 없기 때문이다.

   ```java
    class 이주언 {
        int numberOfHairs = 100;

        int 탈모(int numberOfLostHairs) {
            numberOfHairs -= numberOfLostHairs;
            return numberOfHairs;
        }

        이주언() {
            탈모(10);
        }

        void printNumberOfHairs() {
            System.out.println("이주언 has only " + numberOfHairs + " hairs.");
        }
    }

    public class stress {
        public static void main(String[] args) {
            이주언 이주언 = new 이주언();
            이주언.탈모(5);
            이주언.printNumberOfHairs();
        }
    }

    // 출력: 이주언 has only 95 hairs.
   ```

   `이주언` class에서는 `탈모()`의 호출을 위해 `이주언()` constructor를 이용하여 객체가 생성될 때 `탈모()`가 실행되게끔 하였다.

   `stress` class에서는 `이주언` class의 `탈모()`와 `printNumberOfHairs()` method를 호출하기 위하여 `이주언`의 instance를 새로 생성하였다.

4. overloading

   Class 내의 같은 이름의 method를 다수 선언하는 것을 method overloading이라고 한다. 두 개 이상의 method 이름이 같으므로, 매개변수의 type, 개수, 순서 중 하나 이상이 달라야 한다. Overloading은 매개값을 다양하게 받아 각각 알맞게 처리할 수 있도록 하게 해준다.

   예를 들어 다음과 같은 method가 있다고 할 때,

   ```java
   int add(int firstNum, int secondNum) {
     return firstNum + secondNum;
   }
   ```

   `add()` method를 호출하기 위해서는 두 개의 `int` type parameter들이 필요하다. 하지만 `double` type 값의 덧셈 연산을 할 때에는 이 method를 호출하지 못한다. 같은 class 내에 같은 동작을 하는 `double`로 선언된 method를 만들면 이를 해결할 수 있다.

   ```java
   double add(double firstNum, double secondNum) {
      return firstNum + secondNum;
   }
   ```

   Overloading 된 method를 호출할 경우 parameter의 타입을 보고 실행 할 method를 결정한다. 가령, 아래와 같이 메소드를 호출하면 `int`로 선언된 `add()`가 실행될 것이다.

   ```java
   add(7, 8)
   ```

   만약 다음과 같이 두 매개변수의 자료형이 애매하게 일치하지 않을 경우, 자동 타입 변환이 가능한지를 검사한다.

   ```java
   add(16, 7.5)
   ```

   위와 같은 경우 첫 번째 매개변수의 type인 `int`는 `double`로 형변환이 가능하므로, `double`로 선언된 `add()`가 실행되게 된다.

---
