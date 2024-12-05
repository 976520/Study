## 스프링에 그거 ㅇㅇ

1.  이해

    > 객체의 의존성을 런타임 시 외부에서 주입하는 방법이다.

    Dependency Injection은 객체 간의 의존 관계가 소스 코드 외부에서 설정을 통해 정의되는 pattern이다.

    Dependency는 다음과 같이 한 객체가 다른 객체를 사용할 때 발생하는 것이다.

    ```java
    class Service {
    }

    class Client {
        private Service service;

        public Client(Service service) {
            this.service = service;
        }
    }
    ```

    이 경우 Service와 Client가 강하게 결합되어 있다.

    다음 그림에서는 Client가 Service를 사용하고 있으므로, Client는 Service에 대한 dependency를 가지고 있다.

    <img src="https://github.com/user-attachments/assets/b83e74ea-27b9-4285-960e-4e9850b53cfd" alt="image" width="500" />

    여기서 Injector는 DI container라고도 불리며, 객체 간의 **의존성을 관리하고 주입**하는 역할을 담당하는 구성 요소이다. Dependency Injection pattern에서는 Injector가 Client 객체에게 필요한 의존성, 즉 Service 객체를 직접 생성하여 제공한다. 이로써 Client는 자신이 필요로 하는 의존성을 스스로 생성하거나 관리할 필요가 없어지며, 대신 Injector가 모든 의존성의 생성과 관리를 전담하게 된다.

    Injector가 이러한 역할을 수행하기 위해서는 각 객체 간의 의존 관계와 생성에 필요한 정보를 알고 있어야 한다. 예를 들어, Client 객체를 생성할 때 어떤 Service 객체를 주입해야 하는지, 그리고 해당 Service 객체를 생성하기 위해 필요한 생성자 인자가 무엇인지 등을 파악하고 있어야 한다.

    자신의 의존 관계조차 마음대로 결정할 수 없는 Client 객체의 눈물어린 희생 덕분에, 코드의 결합도가 크게 낮아져 유연성과 테스트 용이성이 높아진다.

2.  사용

    상술한 예제를 코드로 구현하면 다음과 같다.

    ```java
    class Service {
    }

    class Client {
        private final Service service;

        public Client(Service service) {
            this.service = service;
        }
    }

    class Injector {
        public static Client getClient() {
            Service service = new Service();
            return new Client(service);
        }
    }
    ```

    위 코드에서 `Service` class는 `Client` class가 의존하는 객체이다.

    `Client` class는 생성자를 통해 `Service` 객체를 주입받는다. 이때 `final` 키워드를 사용하여 `service` field가 한 번 할당되면 변경되지 않도록 한다.

    `Injector` class의 `getClient()` method에서 `Service` 객체를 직접 생성하고, 이를 `Client` 생성자에 전달하여 `Client` 객체를 생성한 후 반환한다.

---
