# 객체 지향 프로그래밍

> OOP(Object Oriented Programming)은 프로그램을 수많은 객체(object)라는 기본 단위로 나누고 이들의 상호 작용으로 서술하는 방법론이다.

우선 객체에 대해 이해해야 한다.

---

## 개념

1. 객체

   현실 세계에서의 객체는 구체적인 사물 혹은 추상적인 개념을 뜻한다. 또한 객체는 state(상태)와 behaver(동작)으로 구성된다. 예를 들어 이주언 이라는 객체는 '서 있음', '앉아 있음' 과 같은 state, '서다', '앉다' 와 같은 behaver으로 구성되어 있다.

   소프트웨어에서의 객체도 비슷한 원리를 지닌다. 단지 state가 field로, behaver가 method로 정의되어있을 뿐이다. field는 객체를 통하여 사용할 수 있는 변수이며, method는 객체를 통하여 호출할 수 있는 동작이다.

   현실 세계의 객체는 개별적으로 사용할 수 있고, 다른 객체와 상호작용할 수도 있다. 예를 들어 이주언이 권재헌을 때리면 이주언에게는 쾌감이, 권재헌에게는 통증이 발생하듯이, 현실 세계에서 발생하는 여러 현상은 객체가 서로 상호작용하여 발생한다.

   소프트웨어에서도 객체는 개별적으로 사용하거나 다른 객체와의 관계를 맺으며 동작할 수 있다. 대부분의 소프트웨어는 다수의 객체로 구성되며, 이들이 상호작용하여 문제를 해결한다. 이러한 문제 해결 방식을 취한 프로그램을 작성하는 것이 OOP라고 할 수 있다.

   OOP에서는 현실 세계를 객체 단위로 프로그래밍한다. 소프트웨어에서 객체는 데이터, 즉 field와 그의 동작 method를 묶어 표현하는 구성 요소라고 정리할 수 있다.

2. Procedural programming(절차적 프로그래밍)과의 비교

   Procedural programming은 동작을 순서에 맞추어 단계적으로 실행되도록 명령어를 나열한다. 데이터의 정의보다 명령의 순서와 흐름에 중점을 둔다. 소규모 프로젝트의 경우 수행할 작업을 예측할 수 있어 직관적이고 프로그래밍하기 쉽다는 장점이 있다.

   하지만 프로젝트 규모의 증대에 따라 이에 따른 한계가 부각될 것이다. 서로 복잡하게 얽힌 데이터를 그의 동작과 분리하여 사용하였기 때문에 추후 변경이나 확장에 난관을 겪을 수 밖에 없다.

   현실 세계의 작업은 절차나 과정보다는 이와 관련한 많은 객체의 상호작용으로 표현하는 것이 효과적이다. 이러한 현실 세계의 특성을 고려하고 procedural programming의 한계를 극복한 것이 OOP이다.

3. class

   제품을 만들기 위해 재료와 함께 설계도가 필요하다. 전통적으로 이를 붕어빵으로 예를 들어 설명한다. 붕어빵이라는 객체는 반죽, 앙금 등의 재료로 만들어지지만, 이것들을 붕어빵으로 만들기 위해서는 붕어빵 형틀(template)가 불가결적이다. OOP의 class가 이 동일한 객체를 생산하는 틀 혹은 설계도라고 할 수 있다.

   Class라는 틀로 만든 객체가 해당 클래스의 instance이다. 예를 들어 붕어빵은 붕어빵 형틀의 instance가 된다. 이와 같이 클래스에서 객체를 생성하는 과정을 instantiation이라고 한다.

   객체는 field와 method로 구성되므로, class도 field와 method를 정의해놓아야 한다. OOP에서는 class의 field와 method를 정의한 후 이를 기반으로 필요한 객체를 생성한다.

---

## 요소

1. 캡슐화(encapsulation)

   변수와 메서드를 하나의 단위로 묶는 것을 의미하며, 이를 데이터의 캡슐화라고 할 수 있습니다. 자바에서는 클래스(class)를 통해 이를 구현하고, 해당 클래스의 인스턴스를 생성하여 클래스 안의 멤버 변수와 메서드에 쉽게 접근할 수 있다.

   > 정보 은닉(information hiding)은 프로그램의 세부 구현을 외부로 드러나지 않도록 특정 모듈 내부로 감추는 것이다.

   캡슐화의 의의는 이 정보 은닉에 있다. 컴퓨터 본체의 부품이 모두 노출된다면 실수로 쉽게 고장을 낼 수 있으므로 부품을 케이스에 담아 보호하는 것과 같은 목적이다. Java에서도 외부로부터 보호하고 싶은 field나 method가 있다면 캡슐화함으로써 외부에서 접근할 수 없도록 사용 범위를 제한할 수 있다. 일반적으로 다음 세 종류의 접근 지정자(access modifier)가 사용된다.

   1. `public`

      Class의 외부에서 사용 가능하도록 노출시킨다. 한마디로 어디서든 접근할 수 있다.

   2. `protected`

      다른 class에게는 노출하지 않지만 동일 패키지 내의 class나, 상속받은 하위 class에게는 노출한다. 다른 패키지의 class에게는 노출되지 않는다.

   3. `default`

      `protected`와 동일하게 동일 패키지 내의 class에게 노출한다. 그러나 하위 class에게 노출하지 않는다.

   4. `private`

      클래스의 내부에서만 사용하며 외부로 노출하지 않는다.

   컴퓨터의 RAM이 고장 났을 때 다른 RAM으로 교체하면 정상적으로 작동한다. 마찬가지로 class 내부의 캡슐화된 코드는 독립적으로 관리되어 동일한 기능이라면 다른 코드로 대체될 수 있다. 이를 통해 코드의 모듈화 편의성과 재사용성을 높일 수 있다.

2. 상속(inheritance)

   상속은 하위 객체가 상위 객체의 특성과 기능을 물려받는 것을 뜻한다. 상속받은 하위 객체가 상위 객체의 method와 field를 사용할 수 있게 되며, 이는 재사용성을 높인다.

   이때 상위 객체 class를 parent(부모) class, super class, base(기본) class 라고 하기도 하며, 하위 객체 class를 child(자식) class, subclass, derived(파생) class, extended(확장) class라고 하기도 한다.

   **Overriding은 하위 class가 상위 class에서 상속받은 method를 자신에게 맞게 재정의하는 것**을 말한다. 예를 들어 human이라는 class를 상속받아 권재헌, 이주언, 황지훈 등 하위 class를 추가할 수 있다. 상위 class의 method를 그대로 사용하지 않고, 하위 class의 상황에 맞게 동작하도록 변경할 수 있다. overriding된 method는 하위 class에서 호출될 때, 상위 class의 method가 아닌 하위 class에서 재정의된 method가 실행된다.

   다른 예시로, human class에 greet()라는 method가 있다고 가정하면, 이주언 class는 이 method를 overriding하여 "hello, i'm 이주언."라고 인사하도록 변경할 수 있다. 이때 권재헌 class는 "hello, i'm nigga."와 같이 다르게 overriding할 수 있다. 이러한 overriding을 통해 코드의 유연성과 확장성을 높일 수 있다.

3. 다형성(polymorphism)

   > 다형성은 대입되는 객체에 따라서 method를 다르게 동작하도록 구현하는 것이다.

   하나의 method가 상황에 따라 다른 의미로 해석될 수 있는 것을 일컫는다. 다른 객체에서도 동작이 비슷하면 다형성을 이용해 코드를 간결하게 작성할 수 있다. 권재헌과 이주언은 서로 다르게 인사한다. 따라서 human class의 greet() method를 하위 class에서 수정한다면 각 객체에 적합하게 이용할 수 있게 된다. greet()를 전달하는 것은 동일할지라도 사람마다 다르게 반응하도록 하는 것이다. 이렇듯 동일하게 명령해도 객체에 따라 다른 결과가 나타나도록 하는 것이 다형성이다.

---

## 원칙

OOP에서 지켜야 하는 5가지 원칙을 통틀어 객체지향 5원칙이라고 부른다. 각 원칙의 앞글자를 따서 SOLID라고 하기도 한다.

1. Single Responsibility Principle(단일 책임 원칙)

   > 객체는 오직 하나의 책임을 지녀야 한다.

   하나의 객체는 오직 하나의 기능을 수행하여야 한다. 만일 하나의 객체가 여러 기능을 수행하게 된다면, 다른 기능을 수행하는 코드끼리 클래스 내부에서 결합하여 코드의 변경이 일어났을 때 그것이 영향을 끼치는 기능이 많아지게 된다.

   따라서 책임이란 변경의 이유와 동일하다. 이 원칙을 따름으로써 각 class 주제에 적합한 알맞은 책임을 부여한다면, 한 책임의 변경으로부터 다른 책임의 변경이 일어나고 이것이 반복되는 연쇄 작용을 방지할 수 있다. 여기서 class명까지 기능에 맞게 잘 작성한다면 더 좋을 것이다.

   이 원칙의 핵심은 class의 책임을 최대한 분산시키고 기능 변경 시의 파급 효과를 최소화하여 유지보수성을 증대시키는 것에 있다.

   아래 코드는 유저 정보의 유효성을 검사하고 관리하는 기능을 수행한다. 이때 유저 정보의 유효성 검사 기능은 `UserValidator` class의 `validateEmail` method에서 수행하고 유저 정보의 저장과 관리 기능은 `User` class의 `User` method에서 수행한다.

   ```java
    class User {
        private String name;
        private String email;

        public User(String name, String email) {
            this.name = name;
            this.email = email;
        }

        public String getName() {
            return name;
        }

        public String getEmail() {
            return email;
        }
    }

    class UserValidator {
        public boolean validateEmail(User user) {
            String email = user.getEmail();
            return email != null && email.contains("@");
        }
    }

    public class Main {
        public static void main(String[] args) {
            User user = new User("haensol", "haensol@naver.com");

            UserValidator validator = new UserValidator();
            boolean isEmailValid = validator.validateEmail(user);

            if (isEmailValid) {
                System.out.println("valid.");
            } else {
                System.out.println("invalid.");
            }
        }
    }

   ```

   이때 `UserValidator` class가 다음과 같이 변경된다고 가정한다.

   ```java

    class UserValidator {
      public boolean validateEmail(User user) {
          String email = user.getEmail();
          return email != null && email.contains("@");
      }

      public void printUserName(User user) {
          System.out.println(user.getName());
      }
    }
   ```

   기존 class에서 `printUserName` method가 유저 이름의 출력이라는 전혀 다른 기능을 수행하고 있으므로, 이는 single responsibility principle를 위반한다고 할 수 있다.

2. Open-Closed Principle(개방 폐쇄 원칙)

   > 객체는 확장에 대해서는 개방적이고 수정에 대해서는 폐쇄적이어야 한다.

   기능이 변하거나 확장하는 것은 자유로워야 하지만, 그 과정에서 기존의 코드가 수정되는 것에서는 신중해야 한다. 한가지 예시로 라이브러리를 들 수 있다. 라이브러리를 사용하는 class의 기능이 변경된다고 해서 라이브러리의 코드가 변경되지는 않는다.

   만약 하나의 객체를 수정해야 할 때 해당 객체에 의존하는 다른 객체들까지 연쇄적으로 수정하게 된다면, 이는 유지보수성이 좋은 설계라고 할 수 없다. 따라서 객체간의 의존성을 최소화하여 코드 변경에 따른 영향력을 최소화하여야 한다.

3. Liskov Substitution Principle(리스코프 치환 원칙)

   > 하위 클래스는 언제나 자신의 상위 클래스를 대체할 수 있다.

   상위 클래스가 들어갈 자리에 하위 클래스를 위치시켜도 단순히 컴파일이 성공하는 것을 넘어서 계획대로 작동해야 한다.

4. Interface Segregation Principle(인터페이스 분리 원칙)

   > 클라이언트에서 사용하지 않는 메서드는 사용해선 안 된다.

5. Dependency Inversion Principle(의존성 역전 원칙)

   > 추상성이 높고 안정적인 고수준의 클래스는 구체적이고 불안정한 저수준의 클래스에 의존해서는 안 된다.

---
