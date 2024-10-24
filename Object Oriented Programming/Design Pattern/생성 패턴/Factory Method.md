## 팩토리 메서드

1. 이해

   > 상위 class에 알려지지 않은 구체 class를 생성하는 pattern이다.

   Instance를 생성하는 factory class를 만들고, 이를 상속하는 하위 factory class의 method에서 여러가지 instance를 생성하는 방식으로 구현된다. 하위 class가 어떤 instance를 생성할 지 결정하게 된다. 즉 객체 생성이라는 책임을 하위 class에게 위임한 것이다.

   객체 생성에 필요한 과정을 template처럼 미리 설계하고, 객체 생성에 관한 전처리나 후처리를 통해 이 과정을 다양하게 처리하여 객체를 유연하게 생성할 수 있게 한다. 때문에 객체를 생성하는 과정을 구현한 코드를 수정하지 않고 새로운 instance 다르게 생성하도록 확장할 수 있으며, 이는 OCP 원칙을 잘 준수했다고 할 수 있다. 이러한 면에서 template method pattern과 유사하고 볼 수 있다.

   또한, factory method pattern을 사용하면 객체 생성 코드와 객체 사용 코드를 분리할 수 있어 결합도를 낮출 수 있다. 이는 코드의 유지보수성을 높이고, 변경에 유연하게 대응할 수 있게 한다.

2. 사용

   ```python
   from abc import ABC, abstractmethod

   class Creator(ABC):
       @abstractmethod
       def factory_method(self):
           pass

       def some_operation(self):
           product = self.factory_method()
           product.use()

   class ConcreteCreatorA(Creator):
       def factory_method(self):
           return ConcreteProductA()

   class ConcreteCreatorB(Creator):
       def factory_method(self):
           return ConcreteProductB()

   class Product(ABC):
       @abstractmethod
       def use(self):
           pass

   class ConcreteProductA(Product):
       def use(self):
           print("im product A")

   class ConcreteProductB(Product):
       def use(self):
           print("im product B")

   if __name__ == "__main__":
       creator_a = ConcreteCreatorA()
       creator_a.some_operation()

       creator_b = ConcreteCreatorB()
       creator_b.some_operation()

   '''
   출력:
   im product A
   im product B
   '''
   ```

   추상 method `factory_method`는 객체 생성의 책임을 가지고 있으며, 하위 class에서 구체적으로 구현되게 된다. `some_operation()`는 factory method를 호출하여 객체를 생성하고 `use()`로 사용하는 메서드이다.

   `ConcreteCreatorA`와 `ConcreteCreatorB`는 `Creator` class를 상속받아 `factory_method`를 구체적으로 구현하고 있다. 이는 각각 `ConcreteProductA`와 `ConcreteProductB`를 생성하는 방식이 다르다는 것을 의미한다. `Product` class는 추상 class로 추상 method `use()`를 가지고 있다. `ConcreteProductA`와 `ConcreteProductB`는 `Product` class를 상속받아 `use()`를 구체적으로 구현하고 있다.

   구체적인 제품 class인 `ConcreteProductA`와 `ConcreteProductB`는 `Product`를 상속받아 각각 다른 방식으로 `use()`를 구현하고 있다.

---
