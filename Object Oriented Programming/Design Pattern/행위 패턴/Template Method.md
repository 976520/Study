## 템플릿 메소드

1. 이해

   > 구조를 변경하지 않고 알고리즘의 특정 단계들을 다시 정의할 수 있게 해주는 pattern이다.

   Template method pattern은 **여러 class에서 공통으로 사용하는 method를 template화 하여 상위 class에서 정의하고, 하위 class에서 재정의하여 세부 동작을 다르게 구현**하는 pattern이다. 즉, 기능의 뼈대(template)와 실제 구현을 분리한다고 할 수 있다. 상속이라는 기능을 극대화하여 알고리즘의 layout을 맞추는 것에 포커스를 둔다.

   이때 template는 변하지 않는 것을 의미한다. 따라서 변하지 않을 기능만을 추상 class에 정의하고, 변하거나 확장될 수 있는 기능은 구현 class에서 추상 method를 override하여 작성한다.

   알고리즘이 단계별로 나누어져야하는 상황이거나, 같은 역할을 하는 method가 여러 곳에서 다른 형태로 사용될 경우 유용하게 사용할 수 있다.

   1. hook method

      추상 class에서 선언하여 하위 class에서 override 하도록 기본적인 것만 구현하거나 비워놓는 method를 의미한다.

   2. dependency rot

      의존성이 심하게 얽혀 복잡하게 꼬여 있는 상황을 의미한다.

2. 사용

   1. python

      ```python
        from abc import ABC, abstractmethod

        class TemplateMethod(ABC):
            def template_method(self):
                self.step1()
                self.step2()
                self.step3()

            @abstractmethod
            def step1(self):
                pass

            @abstractmethod
            def step2(self):
                pass

            @abstractmethod
            def step3(self):
                pass

        class ConcreteClass(TemplateMethod):
            def step1(self):
                print("Step 1")

            def step2(self):
                print("Step 2")

            def step3(self):
                print("Step 3")

        ConcreteClass().template_method()
      ```

      `TemplateMethod` class는 ABC(Abstract Base Class)로, base class를 상속받는 class가 반드시 base class의 method를 구현하도록 강제된다. 이때 `@abstractmethod`를 사용하여 해당 method가 반드시 구현되어야 한다는 것을 명시한다. 이 코드의 `step1`, `step2`, `step3` method가 이에 해당하며, `template_method`에서 이 세 method를 호출하여 알고리즘의 흐름을 정의한다.

   2. java

      ```java
      abstract class TemplateMethod {
          public void templateMethod() {
              step1();
              step2();
              step3();
          }

          protected abstract void step1();
          protected abstract void step2();
          protected abstract void step3();
      }

      class ConcreteClass extends TemplateMethod {
          @Override
          protected void step1() {
              System.out.println("Step 1");
          }

          @Override
          protected void step2() {
              System.out.println("Step 2");
          }

          @Override
          protected void step3() {
              System.out.println("Step 3");
          }
      }

      public class Main {
          public static void main(String[] args) {
              ConcreteClass concreteClass = new ConcreteClass();
              concreteClass.templateMethod();
          }
      }
      ```

      추상 class `TemplateMethod`는 추상 method `templateMethod`를 선언하고, 이를 구현한 `step1`, `step2`, `step3` method를 선언한다. 이때 `step1`, `step2`, `step3` method는 `abstract`로 선언되어 있으므로 반드시 하위 class에서 구현되어야 한다.

   두 코드에서 모두 `ConcreteClass`는 `TemplateMethod`를 상속받아 각 method를 구현한다.

---
