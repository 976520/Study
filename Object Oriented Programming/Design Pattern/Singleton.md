## 싱글톤

1. 이해

   > 객체의 instance를 오직 1개만 생성되게 하는 pattern이다.

   Singleton pattern을 따르는 class는 constructor가 여러 번 호출되더라도, 실제로 생성된 객체는 하나이다. 최초 생성 이후에 호출된 constructor는 최초의 constructor가 생성한 객체를 return한다.

   이렇게 되면 하나의 instance만을 고정 메모리 영역에 생성하고, 이후에 생성되는 instance는 이미 생성된 instance를 가리키는 포인터를 가지게 된다. 때문에 추후 해당 instance에 접근하는 경우 메모리 낭비를 방지할 수 있으며, 속도 측면에서도 이점을 가진다.

   Singleton pattern으로 생성한 instance는 전역 변수처럼 사용할 수 있다. 따라서 여러 class에서 데이터를 공유하는 경우 유용하게 사용할 수 있다. 하지만 동시성 issue가 발생할 수 있으므로 주의해야 한다.

2. 사용

   Singleton pattern의 기본적인 구현은 다음과 같다.

   ```python
   class Singleton:
      obj = None

      @classmethod
      def get_instance(cls):
         if not cls.obj:
               cls.obj = cls()
         return cls.obj

   singleton1 = Singleton.get_instance()
   singleton2 = Singleton.get_instance()

   print(singleton1 is singleton2)  # 출력: True
   ```

   `obj`는 class 변수로, class 내에서 여러 instance가 공유하는 변수이다.

   `get_instance()` method에서는 이미 생성된 instance가 있는 경우 이를 반환하고, 없는 경우 생성 후 반환한다. 이때 `@classmethod`를 사용하는 이유는 class method로 선언하여 instance를 생성하지 않고도 class method를 호출할 수 있도록 하기 위함이다.

   ```java
   public class Singleton {
      private static Singleton obj;

      private Singleton() {}

      public static Singleton getInstance() {
         if (obj == null) {
            obj = new Singleton();
         }
         return obj;
      }
   }

   Singleton singleton1 = Singleton.getInstance();
   Singleton singleton2 = Singleton.getInstance();

   System.out.println(singleton1 == singleton2); // 출력: true
   ```

   `getInstance()` 메소드를 통해 instance를 생성하고, 이미 생성된 instance가 있다면 해당 instance를 반환한다. 이때 private으로 선언된 constructor를 사용하여 외부에서 instance를 생성하는 것을 방지한다.

   따라서 두 코드에서 모두 `singleton1`과 `singleton2`는 같은 instance를 가리키는 포인터를 가지게 된다.

---
