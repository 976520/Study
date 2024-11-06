## model-view-presenter pattern

1. 이해

   MVP pattern은 전통적인 MVC pattern의 변형으로, MVC pattern에서의 controller 역할을 presenter가 대신 수행하는 구조이다.

   MVP pattern은 UI와 business logic을 명확히 분리하여 application의 유지보수성과 테스트 용이성을 높이는 것을 목적으로 한다. MVP pattern의 구성 요소는 다음과 같이 세 가지로 나눌 수 있다.

   1. model

      MVC pattern과 대부분 유사하게 데이터를 관리하고 business logic을 처리하는 계층이다.

      MVP pattern에서는 view로부터 직접 데이터 요청을 받는 것이 아니라 presenter를 통해 data에 access하게 된다. 이를 통해 model은 view나 presenter에 대한 의존성을 가지지 않는다.

   2. view

      UI를 담당하는 계층으로, 사용자로부터의 입력을 받고 결과를 표시하는 역할을 한다.

      MVP pattern에서는 view가 model로부터 직접 data를 가져오지 않고, presenter를 통해 필요한 data를 받는다. 이는 view가 business logic과 분리되어 오로지 UI 관련 코드에만 집중할 수 있도록 도와준다.

   3. presenter

      Model과 view 사이의 중재자로서, 사용자 입력을 처리하고 필요한 data를 model로부터 가져와서 view에 전달하는 역할을 수행한다.

      Presenter는 view에 대한 참조를 가지고 있으나, view의 구체적인 구현에 의존하지 않고 interface를 통해 통신함으로써 테스트 용이성을 높인다. 또한, presenter는 view와 model 간의 상호작용을 관리하며, business logic을 수행하여 application의 전체적인 흐름을 제어한다. 이때, 각 view와 presenter는 **일대일로 연결**되어 독립적으로 동작할 수 있도록 설계된다.
