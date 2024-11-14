## 프록시 서버는 아는데

1. 이해

   > 객체가 처리를 직접 하지 않고 중간에 숨겨진 다른 객체를 통해 처리하는 방법이다.

   Client가 대상 객체를 직접 사용하는 것이 아니라, 대리인(proxy)을 거쳐서 쓰는 pattern이다. 따라서 subject의 method에 접근하기 위해 proxy 객체의 method에 접근한 후 추가적인 logic을 수행한 뒤 접근하게 된다. 때문에 client가 객체를 신경쓰지 않고 service 객체를 제어할 수 있다.

   이를 통해 다음과 같은 이점을 가질 수 있다.

   1. Security

      Proxy는 client가 대상 객체에 접근할 권한이 있는지 확인한다. 이를 통해 불법적인 접근을 차단하고, 보안을 강화할 수 있다.

      예를 들어 인증된 사용자만이 특정 객체에 접근할 수 있도록 제한할 수 있다.

   2. Caching

      Proxy는 data가 cache에 없을 때만 작업이 실행되도록 한다. 작업 결과를 caching하여 중복 처리를 방지할 수 있다. 이를 통해 성능을 최적화하고, 동일한 요청에 대해 빠른 응답을 제공할 수 있다.

      예를 들어 DB 조회 결과를 캐싱하여 반복적인 조회를 줄일 수 있다.

   3. Data processing

      Proxy는 데이터를 처리하거나 변환하는 역할을 할 수 있다.

   4. Lazy initialization

      객체의 생성 및 초기화를 지연시키고 필요한 순간에 해서 성능을 최적화 할 수 있다. 이를 통해 불필요한 resource 낭비를 줄이고, 초기 loading 시간을 단축할 수 있다.

      예를 들어 대용량 객체를 실제로 필요할 때까지 생성하지 않고, 요청이 있을 때 생성할 수 있다.

   5. Logging

      Proxy는 method 호출과 상태 매개 변수를 intercept하고 이를 기록한다. 이를 통해 system의 동작을 추적하고, 문제 발생 시 디버깅을 용이하게 할 수 있다.

   6. Remote object

      Proxy는 local이 아닌 원격에 있는 객체를 가져와서 local처럼 사용할 수 있다. 이를 통해 분산 system에서 원격 객체와의 통신을 투명하게 처리할 수 있다.

   기존 객체 코드를 변경하지 않고 새로운 기능을 추가할 수 있기 때문에 Open-Closed Principle을 준수하며, 대상 객체가 자신의 기능에만 집중하고, 그 이외의 기능을 proxy에 위임하기 때문에 Single Responsibility Principle을 준수한다.

2. 사용

   ```java
    interface Subject {
        void request();
    }

    class RealSubject implements Subject {
        @Override
        public void request() {
            System.out.println("RealSubject, Handling");
        }
    }

    class Proxy implements Subject {
        private RealSubject realSubject;

        @Override
        public void request() {
            if (realSubject == null) {
                realSubject = new RealSubject();
            }
            System.out.println("Proxy, Logging");
            realSubject.request();
        }
    }

    public class Client {
        public static void main(String[] args) {
            Proxy proxy = new Proxy();
            proxy.request();
        }
    }

    /*
    출력:
    Proxy, Logging
    RealSubject, Handling
    */
   ```

   `Subject` interface는 `request` method를 정의하고, `RealSubject` class는 `Subject` interface를 구현하며, `request` method를 실제로 처리하는 역할을 한다.

   `Proxy` class는 `Subject` interface를 구현하며, `RealSubject` 객체를 참조하고, `request` method를 호출할 때, `RealSubject` 객체가 생성되지 않았다면 생성하고, logging, 즉 추가적인 logic을 수행한 후 `RealSubject`의 `request` method를 호출한다.

   `Client` class는 `Proxy` 객체를 생성하고, `request` method를 호출한다. 이를 통해 `Proxy` 객체가 `RealSubject` 객체의 `request` method를 호출하기 전에 logging을 수행하는 것을 확인할 수 있다.

---
