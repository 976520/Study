## 원칙

OOP에서 지켜야 하는 5가지 원칙을 통틀어 객체지향 5원칙이라고 부른다. 각 원칙의 앞글자를 따서 SOLID라고도 한다.

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
                System.out.println("ㅆㄱㄴ");
            } else {
                System.out.println("컷ㅋ");
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

   아래 코드에서는 `Shape` interface와 이를 구현한 `Circle`, `Rectangle` class를 통해 프로그램을 확장한다. 이 과정에서 기존의 `AreaCalculator` class 내부 코드를 변경하지 않았으므로 open closed principle 원칙을 지켰다고 할 수 있다.

   ```java
    interface Shape {
        double calculateArea();
    }

    class Circle implements Shape {
        private double radius;

        public Circle(double radius) {
            this.radius = radius;
        }

        @Override
        public double calculateArea() {
            return Math.PI * radius * radius;
        }
    }

    class Rectangle implements Shape {
        private double width;
        private double height;

        public Rectangle(double width, double height) {
            this.width = width;
            this.height = height;
        }

        @Override
        public double calculateArea() {
            return width * height;
        }
    }

    class AreaCalculator {
        public double calculateTotalArea(Shape[] shapes) {
            double totalArea = 0;
            for (Shape shape : shapes) {
                totalArea += shape.calculateArea();
            }
            return totalArea;
        }
    }

    public class Main {
        public static void main(String[] args) {
            Shape[] shapes = new Shape[] {
                new Circle(5),
                new Rectangle(4, 6)
            };

            AreaCalculator calculator = new AreaCalculator();
            double totalArea = calculator.calculateTotalArea(shapes);
            System.out.println(totalArea);
        }
    }
   ```

3. Liskov Substitution Principle(리스코프 치환 원칙)

   > 하위 클래스는 언제나 자신의 상위 클래스를 대체할 수 있다.

   상위 class가 들어갈 자리에 하위 class를 위치시켜도 단순히 컴파일이 성공하는 것을 넘어서 계획대로 작동해야 한다. 이것을 상위 class와 하위 class간의 일관성이 있다고 한다.

   OOP에서 상속이 일어나면, 하위 class는 상위 class의 특성을 가지며 그를 토대로 확장할 수 있지만 상위 class의 기능을 무시하거나 약화시키지 않아야 한다. liskov substitution principle는 올바른 상속을 위해 하위 객체의 확장이 부모 객체의 방향성을 완전히 따르도록 하는 것이다.

   이 원칙을 준수하면 OOP의 요소 중 다형성이 증대되는 효과가 있다.

   아래 코드에서 `Bird` class는 `fly` method를 가지며, 모든 새는 날 수 있다고 가정한다. `Pigeon`, `Penguin` class는 모두 `Bird`를 상속받았지만, `Penguin`은 날 수 없기 때문에 `fly` method를 호출할 때 예외를 throw한다. 이때 하위 class인 `Penguin`이 부모 class의 기대 동작, `fly`를 충족하지 않기 때문에 liskov substitution principle를 위반한다.

   ```java
    class Bird {
        public void fly() {
            System.out.println("날아간다~");
        }
    }

    class Pigeon extends Bird {
        @Override
        public void fly() {
            System.out.println("비둘기, 난다.");
        }
    }

    class Penguin extends Bird {
        @Override
        public void fly() {
            throw new UnsupportedOperationException("펭귄, 못 난다.");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Bird Pigeon = new Pigeon();
            Bird penguin = new Penguin();

            Pigeon.fly();

            penguin.fly();
        }
    }
   ```

4. Interface Segregation Principle(인터페이스 분리 원칙)

   > 클라이언트가 자신이 이용하지 않는 메서드에 의존하면 안된다

   Interface는 동일 목적 하에 동일한 기능을 수행하도록 강제한다. 어떤 class가 특정한 interface를 사용하여 구현된다면, 그 class는 반드시 그 interface에 포함되어있는 method를 구현하도록 하는 것이다. 이는 Java의 다형성을 극대화하여 유지보수성을 높인다.

   Interface segregation principle는 범용적인 interface보다 클라이언트, 즉 사용자가 실제로 사용하는 interface를 만들어야 한다는 의미로, interface를 그 기능에 맞게 분리해야 한다는 원칙이다.

   만약 interface의 추상 method들을 범용적으로 구현한다면, 그 interface를 상속받은 class는 자신이 사용하지 않는 method마저 구현된다는 단점이 있다. 또한 사용하지 않는 interface의 추상 method가 변경된다면 class에서도 수정이 필요해진다. 이는 유지보수성을 크게 하락시킬 수 있다.

   Interface segregation principle은 single responsibility principle와 유사한 면이 있다. 후자가 class의 단일 책임을 위한 원칙이라면, 전자는 interface의 단일 책임 원칙을 강조한다고 할 수 있다. 즉 이 원칙은 class가 아닌 interface의 분리를 통해 이루어진다.

   아래 코드에서는 `Robotics` interface가 `work`와 `eat` method를 포함한다. `용빈` class는 두 method를 모두 구현할 수 있지만, `용빈이의로봇`은 `eat` method를 구현할 필요가 없다. 하지만 interface를 위해 불필요한 `eat`을 구현해야만 한다. 이는 interface segregation principle를 위반한 것이다.

   ```java
    interface Robotics {
        void work();
        void eat();
    }

    class 용빈 implements Robotics {
        @Override
        public void work() {
            System.out.println("용빈이가 훈련을 한다.");
        }

        @Override
        public void eat() {
            System.out.println("용빈이가 급식을 먹는다.");
        }
    }

    class 용빈이의로봇 implements Robotics {
        @Override
        public void work() {
            System.out.println("로봇이 훈련을 한다.");
        }

        @Override
        public void eat() {
            // 로봇은 먹을 수 없다!
        }
    }
   ```

   아래 코드에서는 기존 `Robotics` interface를 기능에 따라 두 개의 작은 interface로 나누었다. 문제가 되었던 `용빈이의로봇` class가 자신에게 필요한 `work`만 구현하여 불필요한 method 구현을 방지하였다.

   ```java
    interface Workable {
        void work();
    }

    interface Eatable {
        void eat();
    }

    class 용빈 implements Workable, Eatable {
        @Override
        public void work() {
            System.out.println("용빈이가 훈련을 한다.");
        }

        @Override
        public void eat() {
            System.out.println("용빈이가 급식을 먹는다.");
        }
    }

    class 용빈이의로봇 implements Workable {
        @Override
        public void work() {
            System.out.println("로봇이 훈련을 한다.");
        }
    }

   ```

5. Dependency Inversion Principle(의존성 역전 원칙)

   > 추상성이 높고 안정적인 고수준의 클래스는 구체적이고 불안정한 저수준의 클래스에 의존해서는 안 된다.

   Dependency inversion principle이란 객체가 어떤 class를 참조해서 사용해야 한다면, 그 class를 직접 참조하는 것이 아닌 그의 상위 요소, 즉 추상 class 혹은 interface로 참조하라는 원칙이다.

   의존 관계란, 한 class가 기능을 수행하려 할 때 다른 class의 기능이 필요한 관계를 뜻한다. 객체들이 서로 정보를 주고 받을 때 의존 관계가 형성된다.

   클라이언트가 상속 관계로 이루어진 모듈을 사용할 때, 하위 모듈을 직접 사용하지 않아야 한다. 하위 모듈의 구체적인 내용에 의존하여 코드를 자주 수정하기보다 상위 interface의 추상적인 내용에 의존하여 코드를 보다 덜 수정하는 것이 유지보수성이 더 높다고 할 수 있다.

   위 코드에서 `Switch`는 `LightBulb`에 직접 의존하고 있다. 만약 `LightBulb`를 다른 class로 교체하려면 `Switch`도 수정해야 한다.

   ```java
    class LightBulb {
        public void turnOn() {
            System.out.println("전구켜짐");
        }

        public void turnOff() {
            System.out.println("전구꺼짐");
        }
    }

    class Switch {
        private LightBulb lightBulb;

        public Switch(LightBulb lightBulb) {
            this.lightBulb = lightBulb;
        }

        public void operate(String command) {
            if (command.equalsIgnoreCase("on")) {
                lightBulb.turnOn();
            } else if (command.equalsIgnoreCase("off")) {
                lightBulb.turnOff();
            }
        }
    }

    public class Main {
        public static void main(String[] args) {
            LightBulb lightBulb = new LightBulb();
            Switch lightBulbSwitch = new Switch(lightBulb);
            lightBulbSwitch.operate("on");
            lightBulbSwitch.operate("off");
        }
    }
   ```

   `Switchable`이라는 interface를 새로 만들고, `LightBulb`와 `Fan`이 이를 구현하도록 한다. `Switch` class는 이제 `Switchable`에 의존하므로, 저수준 모듈이 무엇이든 상관없이 작동할 수 있다. 이 방식으로 `Switch`는 저수준 구현에 의존하지 않으므로, dependency inversion principle를 준수하게 된다. 필요에 따라 새로운 class를 쉽게 추가할 수 있고, 이에 따라 `Switch`는 변경할 필요도 없습니다.

   ```java
    interface Switchable {
        void turnOn();
        void turnOff();
    }

    class LightBulb implements Switchable {
        @Override
        public void turnOn() {
            System.out.println("전구켜짐");
        }

        @Override
        public void turnOff() {
            System.out.println("전구꺼짐");
        }
    }

    class Fan implements Switchable {
        @Override
        public void turnOn() {
            System.out.println("선풍기켜짐");
        }

        @Override
        public void turnOff() {
            System.out.println("선풍기꺼짐");
        }
    }

    class Switch {
        private Switchable device;

        public Switch(Switchable device) {
            this.device = device;
        }

        public void operate(String command) {
            if (command.equalsIgnoreCase("on")) {
                device.turnOn();
            } else if (command.equalsIgnoreCase("off")) {
                device.turnOff();
            }
        }
    }

    public class Main {
        public static void main(String[] args) {
            Switchable lightBulb = new LightBulb();
            Switchable fan = new Fan();

            Switch lightBulbSwitch = new Switch(lightBulb);
            Switch fanSwitch = new Switch(fan);

            lightBulbSwitch.operate("on");
            lightBulbSwitch.operate("off");

            fanSwitch.operate("on");
            fanSwitch.operate("off");
        }
    }
   ```

---
