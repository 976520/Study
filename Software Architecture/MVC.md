## model-view-controller pattern

1. 이해

   <img src="https://github.com/user-attachments/assets/4406a9b1-64b0-40ce-98d3-7d48395f8e83" width="70%" />

   MVC pattern은 system을 model, view, controller의 세 가지 요소로 분리하는 pattern으로, 각 요소는 다음과 같은 기능을 수행한다.

   1. model

      Application의 data를 나타내는 데 사용된다. Database에 저장된 data를 처리하거나, data의 구조를 정의하는 데 사용된다. Model은 data의 상태를 관리하고, data에 대한 모든 logic을 포함한다.

   2. view

      사용자가 보게 될 user interface를 나타내는 데 사용된다. Text, check box, button 등과 같은 UI 요소를 포함한다. View는 model에서 데이터를 가져와 사용자에게 표시한다.

   3. controller

      Model과 View 간의 상호 동작을 관리하는 데 사용된다. 사용자의 입력을 받고, model에 필요한 data를 요청한다. model이 데이터를 처리한 후, 결과를 view에 전달하여 사용자에게 표시한다. Controller는 application의 logic을 포함하고, model과 view 간의 통신을 조정한다.

   사용자가 controller를 조작하면, controller는 model을 통해 data를 가져와 view를 제어하여 사용자에게 표시한다.

   이를 통해 user interface로부터 business logic을 분리하여 application의 시각적 요소나 그 이면에서 구동되는 logic을 독립적으로 개발하고, 서로 영향 없이 수월하게 고칠 수 있는 architecture를 구축할 수 있다.

2. 사용

   ```python
   class Model:
        def __init__(self):
            self.data = "Initial data"

        def get_data(self):
            return self.data

        def set_data(self, new_data):
            self.data = new_data

    class View:
        def display(self, data):
            print(f"View: {data}")

    class Controller:
        def __init__(self, model, view):
            self.model = model
            self.view = view

        def update_model(self, new_data):
            self.model.set_data(new_data)

        def get_model_data(self):
            return self.model.get_data()

        def display_view(self):
            data = self.get_model_data()
            self.view.display(data)

    model = Model()
    view = View()
    controller = Controller(model, view)

    controller.display_view()
    controller.update_model("New data")
    controller.display_view()
   ```

---