## layered pattern

1. 이해

   <img src="https://github.com/user-attachments/assets/3a06d85a-4a94-48a9-81da-7dfe33d81efe" width="70%" />

   Layered pattern은 system을 여러 계층으로 나누어 각 계층이 separation of concerns(관심사의 분리)를 달성하기 위해 특정 기능을 수행하도록 하는 architecture이다. 이러한 구조는 각 계층이 다른 계층과 통신하는 방식으로 작동한다.

   각 계층은 각자의 역할, 즉 자신의 책임에 해당하는 행위만을 수행하도록 분리되어야 한다. Layered architecture에서는 하위 계층에 의존적인 구조이다. 그러나 하위 계층은 상위 계층에 대한 정보를 가지고 있으면 안된다.

   예를 들어 user의 request를 받아 처리하는 presentation layer는 내부 business logic을 수행하는 application layer를 의존한다. 이때 하위 계층인 application layer는 상위 계층인 presentation layer에 대해 몰라야 한다. 단지 간접적으로 넘어온 data를 받아 처리할 뿐이다.

2. 사용

   ```python
    class PresentationLayer:
        def __init__(self, application_layer):
            self.application_layer = application_layer

        def handle_request(self, request):
            processed_request = self.application_layer.process_request(request)
            return processed_request

    class ApplicationLayer:
        def __init__(self, business_logic_layer):
            self.business_logic_layer = business_logic_layer

        def process_request(self, request):
            processed_data = self.business_logic_layer.process_data(request)
            return processed_data

    class BusinessLogicLayer:
        def __init__(self, data_access_layer):
            self.data_access_layer = data_access_layer

        def process_data(self, data):
            processed_data = self.data_access_layer.access_data(data)
            return processed_data

    class DataAccessLayer:
        def access_data(self, data):
            return "data from database"

    data_access_layer = DataAccessLayer()
    business_logic_layer = BusinessLogicLayer(data_access_layer)
    application_layer = ApplicationLayer(business_logic_layer)
    presentation_layer = PresentationLayer(application_layer)

    request = "User request"
    result = presentation_layer.handle_request(request)
    print(f"i'm {result}") # 출력: i'm data from database

   ```

   `PresentationLayer` class는 application 계층과 상호작용하여 사용자의 요청을 처리한다. `ApplicationLayer` class는 business logic 계층과 상호작용하여 요청을 처리한다. `BusinessLogicLayer` class는 data access 계층과 상호작용하여 data를 처리한다. `DataAccessLayer` class는 database에서 data에 access한다..

   `handle_request`, `process_request`, `process_data` method는 이전 계층에서 넘어온 data를 받아 처리하여 반환하는 역할을 한다.

---
