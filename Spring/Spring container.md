## Spring container

> Spring container는 spring framework의 핵심 component이다.

Java에서 `new`를 통해 객체를 생성할 경우, 객체 간의 참조가 많아져 결합도가 높아지게 된다. 이를 낮추기 위해 spring container를 사용한다.

1. 이해

   1. 기능

      Spring container는 **bean의 lifecycle을 관리**하고, bean의 instance화, bean의 구성까지 한다. 또한 생성된 bean에게 추가적인 기능을 제공하는 역할도 한다.

      이렇게 bean을 만들어 관리하고 개발자가 필요할 때 제공한다.

   2. 설정

      Spring container는 XML, annotation 기반의 java configuration class를 통해 설정할 수 있다. 옛날옛적에는 직접 설정해야만 했지만, Spring Boot의 등장으로 그럴 필요가 없어졌다.

   3. 종류

      Spring container는 대표적으로 두 가지가 있다.

      1. ApplicationContext

      1. BeanFactory

---
