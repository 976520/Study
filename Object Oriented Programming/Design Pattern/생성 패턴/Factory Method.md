## 팩토리 메서드

1. 이해

   > 상위 class에 알려지지 않은 구체 class를 생성하는 pattern이다.

   Instance를 생성하는 factory class를 만들고, 이를 상속하는 하위 factory class의 method에서 여러가지 instance를 생성하는 방식으로 구현된다. 하위 class가 어떤 instance를 생성할 지 결정하게 된다. 즉 객체 생성이라는 책임을 하위 class에게 위임한 것이다.

   객체 생성에 필요한 과정을 template처럼 미리 설계하고, 객체 생성에 관한 전처리나 후처리를 통해 이 과정을 다양하게 처리하여 객체를 유연하게 생성할 수 있게 한다. 때문에 객체를 생성하는 과정을 구현한 코드를 수정하지 않고 새로운 instance 다르게 생성하도록 확장할 수 있으며, 이는 OCP 원칙을 잘 준수했다고 할 수 있다. 이러한 면에서 template method pattern과 유사하고 볼 수 있다.

   또한, factory method pattern을 사용하면 객체 생성 코드와 객체 사용 코드를 분리할 수 있어 결합도를 낮출 수 있다. 이는 코드의 유지보수성을 높이고, 변경에 유연하게 대응할 수 있게 한다.

---
