## model-view-presenter pattern

1. 이해

   MVP pattern은 MVC pattern의 변형으로, controller의 역할을 presenter가 대신하는 pattern이다. MVP pattern의 각 요소는 다음과 같다.

   1. model

      MVC pattern과 대부분 동일하지만, data에 대한 요청을 view가 아닌 presenter로부터 받게 된다는 차이점이 있다.

   2. view

      MVC pattern과 대부분 동일하지만, data를 model에서 가져오는 대신 presenter에서 가져온다는 차이점이 있다.

   3. presenter

      Model과 view 사이의 중재자 역할을 하여 상호작용을 관리한다. Model에게 data를 요청하여 가져오거나, data를 업데이트한다. 가져온 data를 view에 전달하여 사용자에게 표시한다.

---
