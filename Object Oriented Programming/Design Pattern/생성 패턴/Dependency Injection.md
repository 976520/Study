## 스프링에 그거 ㅇㅇ

1. 이해

   > 객체의 의존성을 런타임 시 외부에서 주입하는 방법이다.

   Dependency Injection은 객체 간의 의존 관계가 소스 코드 외부에서 설정을 통해 정의되는 pattern이다.

   의존성은 다음과 같이 한 객체가 다른 객체를 사용할 때 발생하는 것이다.

   ```java
   class A {
       private B b;

       public A(B b) {
           this.b = b;
       }
   }
   ```

   다음 그림에서는 Client가 Service를 사용하고 있으므로, Client는 Service에 대한 의존성을 가지고 있다. Dependency Injection pattern에서는 Injector 객체가 Client에게 이 의존성을 주입한다고 할 수 있다.

   <img src="https://github.com/user-attachments/assets/b83e74ea-27b9-4285-960e-4e9850b53cfd" alt="image" width="500" />

---
