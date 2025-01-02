## model-view-template pattern

1. 이해

   MVT pattern은 전통적인 MVC pattern의 변형으로, MVC pattern에서의 controller 역할을 view가 대신 수행하는 구조이다.

   1. model

      MVC pattern과 유사하게 데이터를 관리하는 계층이다.

   2. view

      UI를 담당하는 계층으로, 사용자로부터의 입력을 받고 결과를 표시하는 역할을 한다.

      MVT pattern에서는 view가 controller 역할을 수행하여 business logic을 처리하고, 그 결과를 적절한 template를 통해 사용자에게 응답한다.

   3. template

      Dynamic data를 HTML로 렌더링하여, 사용자에게 보여질 HTML을 제어한다.

2. 사용

   [django](https://github.com/976520/Study/tree/main/Django)

---
