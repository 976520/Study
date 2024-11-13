## Spring container

> Spring container는 spring framework의 핵심 component이다.

Java에서 `new`를 통해 객체를 생성할 경우, 객체 간의 참조가 많아져 결합도가 높아지게 된다. 이를 낮추기 위해 spring container를 사용한다.

1. 이해

   1. 기능

      Spring container는 **bean의 lifecycle을 관리**하고, bean의 instance화, bean의 구성까지 한다. 또한 생성된 bean에게 추가적인 기능을 제공하는 역할도 한다.

      `@ComponentScan` annotation을 통해 특정 패키지 내의 class를 스캔하여 bean으로 등록할 수 있다. `@Component`, `@Service`, `@Repository`, `@Controller` 등의 annotation이 붙은 class도 자동으로 bean으로 등록된다.

      Spring container는 이렇게 bean을 만들어 관리하고 개발자가 필요할 때 제공한다.

   2. 설정

      옛날옛적에는 spring container를 직접 XML로 설정해야만 했지만, Spring Boot의 등장으로 annotation 기반의 java configuration class를 통해 설정할 수 있어졌다.

      `@Configuration` annotation을 통해 class를 configuration class로 설정할 수 있다. Configuration class는 `@Bean` annotation이 붙은 method를 모두 호출하여 bean을 spring container에 등록하는 역할을 한다.

      ```java
      @Configuration
      public class Config {
          @Bean
          public Service service() {
              return new Service();
          }
      }
      ```

   3. 종류

      Spring container는 대표적으로 두 가지가 있다.

      1. BeanFactory

         Spring container의 최상위 interface로, **bean을 관리하고 조회하는 기능**을 제공한다.

      2. ApplicationContext

         BeanFactory를 상속하여 만들어졌으며, 국제화 기능, 환경변수 처리, application event, resource 조회 등 **application 개발을 위한 부가기능을 제공**한다. 다형성이 적용되어 있어, BeanFactory를 상속받은 다른 구현체를 사용할 수 있다.

---
