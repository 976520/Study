# 필드

> 객체의 속성이다.

Field에 대한 원론적인 설명은 [여기](https://github.com/976520/TIL/blob/main/Java/Object%20Oriented%20Programming/%EA%B0%9C%EB%85%90.md)로 redirect 하겠다.

---

## field

1. 이해

   Field는 객체의 데이터를 저장하는 역할을 한다. 여기서 데이터란, 객체의 고유 데이터 뿐만 아니라 객체의 부품 객체, state 등을 모두 포괄한다.

   이주언 객체를 예로 들면 이름과 성별은 고유 데이터에 해당하고, 학교와 학번, 게이 여부는 state에 해당한다. 그리고 머리와 몇 없는 머리카락 등은 부품에 해당할 것이다. 따라서 이주언 class를 설계할 때 이 데이터들을 field로 선언해야 한다.

1. 문법

   `[type] [필드명]( = 초기값);`을 통해 선언할 수 있다. 이 field의 선언은 class의 중괄호 내부 어디서든 존재할 수 있다.

   `[type]`을 통해 field에 저장할 데이터의 종류를 결정할 수 있다. `int`, `float` 등의 기본 type과 배열, class, interface 등의 참조 type이 모두 올 수 있다.

   또한 초기값을 생략할 수 있으며, 초기값이 주어지지 않은 field는 객체 생성 시 기본 초기값으로 설정되게 된다. 이 때 field의 type에 따라 설정되는 초기값이 다르며, 다음은 type이 기본 type일 때 각각의 자료형에 대해 설정되는 초기값을 나열한 것이다.

   1. `byte` `short` `int` 0
   2. `char` \u0000 (공백)
   3. `long` 0L
   4. `float` 0.0F
   5. `double` 0.0
   6. `boolean` false

   참조 type일 때는 `null`값으로 초기화 된다.

1. 사용

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

1. 변수와의 차이

   선언 형태는 일반적인 변수와 비슷할지라도 각각 구분된 개념이다. 그래서 혹자는 field를 class 멤버 변수라고 칭하기도 한다. 객체에 내부의 변수는 constructor 혹은 method 안에서만 사용되며, 이들이 종료되면 자동으로 소멸하게 된다. 하지만 field는 class 안의 constructor와 method 전체에 걸쳐서 사용되며, 객체가 소멸되지 않는 한 계속 존재한다.

---

## final field

1. 이해

   Final field는 보통 field와 달리 초기값이 final value, 즉 최종적인 값이 되어서 실행 도중에 수정이 불가능하다.

2. 문법

   `final [type] [필드명]( = 초기값);`을 통해 선언할 수 있다. `final`이 붙었다는 것 이외에는 일반적인 field와 문법이 동일하다.

   Final field에 초기값을 할당할 수 있는 방법은 다음과 같다.

   1. 최초로 field를 선언할 때 할당

      값이 단순하다면 선언 시에 할당하는 것이 간단하다.

   2. constructor를 통해 할당

      초기화 코드가 복잡하거나, 외부 데이터를 통해 초기화해야 한다면 constructor를 통해 초기값을 지정할 수 있다. 이때 constructor는 final field의 최종 초기화를 반드시 끝마쳐야 한다.

3. 상수

   > 불변의 값을 뜻한다.

   이 불변의 값을 저장하는 field를 java에서도 상수(constant)라고 하는데, final field와는 다음과 같은 차이점들을 갖는다.

   1. 상수는 공용성을 가진다.

   2. 상수는 여러 값으로 초기화될 수 없다.

---
